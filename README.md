# terraform_statefile
# How to manage Terraform State ?
This tutorial would help us to create a S3 bucket and DynamoDB table using terraform in a single file.We shall Know about following topic:-
1.Terraform State.
2.Shared storage for state files.
3.Limitations with terraform Backends.
I got information from this [article](https://blog.gruntwork.io/how-to-manage-terraform-state-28f5697e68fa#.r6xdvtxqe) and the code is explained in this 
[video](https://shorthillstech-my.sharepoint.com/personal/kapil_jain_shorthillstech_com/_layouts/15/onedrive.aspx?ga=1&id=%2Fpersonal%2Fkapil%5Fjain%5Fshorthillstech%5Fcom%2FDocuments%2FTraining%2FDevOps%2F2022%2F45%2Fterraform%20state%5Fkaumudi%2Emp4&parent=%2Fpersonal%2Fkapil%5Fjain%5Fshorthillstech%5Fcom%2FDocuments%2FTraining%2FDevOps%2F2022%2F45)

>Prerequirement:-

- install terraform [video](https://www.youtube.com/watch?v=Cn6xYf0QJME&t=8s)
- Setup your AWS account[video](https://www.youtube.com/watch?v=XhW17g73fvY&t=357s)
- Create IAM user with programmatic access and administrator Access [video](https://www.youtube.com/watch?v=Xx_-IA9qnuI)
- # Steps to run this code
- 1.You need to copy and remove terraform backend block and          outputs from line no.48 to 59 in main.tf file.
![Screenshot (767)](https://user-images.githubusercontent.com/109335469/201523155-66988d98-99ab-481a-8cf9-b8fab935f24f.png)



2.Give unique Bucket_NAME in line no.9 in main.tf file.
 3.Give unique DYNAMODB_TABLE_NAME in line no. 56 in main.tf file
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

![Screenshot (769)](https://user-images.githubusercontent.com/109335469/201523325-988bde68-db24-4194-af89-8da2f264d7f1.png)


7.Run terraform init command then yes (it download provider code, and configure your Terraform backend.After running this command, your Terraform state will be stored in the S3 bucket. You can check this by heading over to the S3 Management Console in your browser and clicking your bucket).

```sh
terraform init
```
8.Now add the outputs code which you copy in first step from line no.62 to 70.(Now backend enabled, Terraform will automatically pull the latest state from this S3 bucket before running a command and automatically push the latest state to the S3 bucket after running a command. To see this in action, that's why we add output variables).

![Screenshot (769)](https://user-images.githubusercontent.com/109335469/201523496-9a0f2a55-a42f-4573-b4df-dd8c5d89b666.png)


9.Run terraform apply command(to see the outputs.Now, go to the S3 console again, refresh the page, and click the Show version button next to Versions. You should now see several versions of your terraform.tfstate file in the S3 bucket).

```sh
terraform apply
```
# STEP TO DESTROY THESE MACHINES:-

1. Remove lifecycle code which we used in S3 bucket in main.tf from line no. 11 to 15
![Screenshot (770)](https://user-images.githubusercontent.com/109335469/201523750-b97612cb-1c82-485e-9b18-f758325fe07c.png)
2.Remove the backend configuration from main.tf from line no.
![Screenshot (767)](https://user-images.githubusercontent.com/109335469/201523858-ce6adca2-64ee-4d24-8652-68c9ff710506.png)
3.Run terraform init-migrate-state command then yes.
```sh
terraform init -migrate-state
```
4.we also  need to remove  versioning objects from S3 bucket.For this open aws s3 console in our browser and  delete that object manually,Select the object then click delete, Enter permanenet delete then click the delete button.

5.Run terraform destroy
```sh
terraform destroy
```



