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