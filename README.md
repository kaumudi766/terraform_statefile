# terraform_statefile
# How to manage Terraform State ?
This article would help us to create a S3 bucket and DynamoDB table using terraform in a single file.We shall Know about following topic:-
1.Terraform State.
2.Shared storage for state files.
3.Limitations with terraform Backends.
I got information from this [article](https://blog.gruntwork.io/how-to-manage-terraform-state-28f5697e68fa#.r6xdvtxqe) and the code is explained in this 
[video](https://www.youtube.com/watch?v=Cn6xYf0QJME)

>Prerequirement:-

- install terraform [video](https://shorthillstech-my.sharepoint.com/personal/kapil_jain_shorthillstech_com/_layouts/15/onedrive.aspx?ga=1&id=%2Fpersonal%2Fkapil%5Fjain%5Fshorthillstech%5Fcom%2FDocuments%2FTraining%2FDevOps%2F2022%2F45%2Fterraform%20state%5Fkaumudi%2Emp4&parent=%2Fpersonal%2Fkapil%5Fjain%5Fshorthillstech%5Fcom%2FDocuments%2FTraining%2FDevOps%2F2022%2F45)
- Setup your AWS account[video](https://shorthillstech-my.sharepoint.com/personal/kapil_jain_shorthillstech_com/_layouts/15/onedrive.aspx?ga=1&id=%2Fpersonal%2Fkapil%5Fjain%5Fshorthillstech%5Fcom%2FDocuments%2FTraining%2FDevOps%2F2022%2F45%2Fterraform%20state%5Fkaumudi%2Emp4&parent=%2Fpersonal%2Fkapil%5Fjain%5Fshorthillstech%5Fcom%2FDocuments%2FTraining%2FDevOps%2F2022%2F45)
- Create IAM user with programmatic access and administrator Access [video](https://shorthillstech-my.sharepoint.com/personal/kapil_jain_shorthillstech_com/_layouts/15/onedrive.aspx?ga=1&id=%2Fpersonal%2Fkapil%5Fjain%5Fshorthillstech%5Fcom%2FDocuments%2FTraining%2FDevOps%2F2022%2F45%2Fterraform%20state%5Fkaumudi%2Emp4&parent=%2Fpersonal%2Fkapil%5Fjain%5Fshorthillstech%5Fcom%2FDocuments%2FTraining%2FDevOps%2F2022%2F45)
- # Steps to run this code
- 1.You need to copy and remove terraform backend block and          outputs from line no.50 to 70 in main.tf file.
2.Give unique Bucket_NAME in line no.10 in main.tf file.
 3.Give unique DYNAMODB_TABLE_NAME in line no. 41 in main.tf file
 4. Run terraform init command (which initialize your code)

```sh
terraform init
```

5.Run terraform apply command (which create aws instance,aws s3
bucket,3 protection layer, and aws dynamodb table).

```sh
terraform apply
```

6.Now add the terraform backend block code which you copy in first step from line no.50 to 61.Give the BUCKET_NAME and DYNAMODB_TABLE_NAME which we create above.
7.Run terraform init command then yes (it download provider code, and configure your Terraform backend.After running this command, your Terraform state will be stored in the S3 bucket. You can check this by heading over to the S3 Management Console in your browser and clicking your bucket).

```sh
terraform init
```
8.Now add the outputs code which you copy in first step from line no.62 to 70.(Now backend enabled, Terraform will automatically pull the latest state from this S3 bucket before running a command and automatically push the latest state to the S3 bucket after running a command. To see this in action, that's why we add output variables).


9.Run terraform apply command(to see the outputs.Now, go to the S3 console again, refresh the page, and click the Show version button next to Versions. You should now see several versions of your terraform.tfstate file in the S3 bucket).

```sh
terraform apply
```