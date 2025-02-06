# Terraform_Course

Terraform Scripts

# Terraform work flow

tf file(.tf) ==> init ==> Validate ==> Plan ==> apply ==> tf state file ==> destory

# Terraform Commands Overview

# 1. Initialization & Formatting

terraform init – Initializes the script by downloading provider-related plugins.
terraform fmt – Formats the script for proper indentation and spacing (optional).

# 2. Validation & Planning

terraform validate – Verifies if the Terraform script is valid.
terraform plan – Creates an execution plan for the script (optional).

# 3. Execution & State Management

terraform apply – Creates resources in the cloud based on the script.
terraform apply --auto-approve
Note: Running this command generates a Terraform state file, which tracks the created resources.

# 4. Destroying Resources

terraform destroy – Deletes the resources created using the Terraform script.

# Types of Variables in Terraform

1. Input Variables

   Used to supply values to the Terraform script.
   Helps in avoiding hardcoded values.
   Example:

   variable "ami" {
   default = "ami-05fa46471b02db0ce"
   }

   variable "instance_type" {
   default = "t2.micro"
   }

   variable "key_name" {
   default = "my-keypair"
   }

   variable "security_group" {
   default = "default"
   }

2. Output Variables

   Used to retrieve values after Terraform execution.
   Helps in getting important details like public IP, bucket info, or database endpoints.

   Example:
   output "ec2_public_ip" {
   value = aws_instance.vm2.public_ip
   }

   output "s3_bucket_name" {
   value = aws_s3_bucket.my_bucket.id
   }

   output "rds_endpoint" {
   value = aws_db_instance.my_rds.endpoint
   }

# What is taint and untaint in terraform

Terraform "taint" is used to replace the resource when we apply the script next time.

For example we have created two resources like below

resource "aws instance"
// configuration

resource 'laws s3 bucket"
// configuration

=> After sometime we realized that ec2 vm got damaged...

Note : we can eintl that ec2 vm using below command to replace when we apply the script next time

$ terraform aint aws instance.vml

$ terraform apply --auto-approve

Note: The alternate for "tain is "replace"

$ terraform apply I-replace=aws instance.vml - -auto-approve

# Terraform Modules

==> A Terraform module is a set of terraform configuration files availal single directory.
==> One module can contain one or more . tf files
        01-Project
            provider.tf
            main.tf
            input-vars.tf
            output-vars.tf

=> One module can have any no. of child modules in terraform
        IRCTC(App)
            - ec2
                main.tf
                input.tf
                output.tf
            - s3
               main.tf
               input.tf
               output.tf
            - rds
                main.tf
                input.tf
                output.tf
            - provider.tf
            - main.tf
            - output.tf

Note : Using terraform modules we can achieve re-usability

Note : We will run terraform commands from root module and root module will invoke child modules for execution.

-------------------------------------
Terraform project setup with Modules
--------------------------------------
### Step—1 : Create Project directory
           Ex: 05-TF-Modu1es

### Step—2 : Create "modules" directory inside project directory
           Ex: 05-TF-Modu1es
                - modules

### Step-3 : Create "ec2" & "s3" directory inside "modules" directory
            Ex: 05-TF-Modu1es
                   - modules
                        - ec2
                        - s3

### Step—4 : Create terraform scripts inside "ec2" directory
            inputs.tf
            main.tf
            outputs.tf

### Step—5 : Create terraform scripts inside "S3" directory
            inputs.tf
            main.tf
            outputs.tf
