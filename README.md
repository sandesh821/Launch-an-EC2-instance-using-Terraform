# Launch-an-EC2-instance-using-Terraform
#Write configuration

#The set of files used to describe infrastructure in Terraform is known as a Terraform configuration. You will write your first configuration to define a single AWS EC2 instance.

#Each Terraform configuration must be in its own working directory. Create a directory for your configuration.

        $mkdir learn-terraform-aws-instance

#Change into the directory.

        $ cd learn-terraform-aws-instance

#Create a file to define your infrastructure.

        $ touch main.tf
 
 #Open main.tf in your text editor, paste in the configuration below, and save the file.
 
         terraform {
          required_providers {
            aws = {
              source  = "hashicorp/aws"
              version = "~> 3.27"
            }
          }

          required_version = ">= 0.14.9"
        }

        provider "aws" {
          profile = "default"
          region  = "us-west-2"
        }

        resource "aws_instance" "app_server" {
          ami           = "ami-830c94e3"
          instance_type = "t2.micro"

          tags = {
            Name = "ExampleAppServerInstance"
          }
        }


#When you create a new configuration — or check out an existing configuration from version control — you need to initialize the directory with

        $ terraform init
                 Initializing the backend...

                Initializing provider plugins...
                - Finding hashicorp/aws versions matching "~> 3.27"...
                - Installing hashicorp/aws v3.27.0...
                - Installed hashicorp/aws v3.27.0 (signed by HashiCorp)

#We recommend using consistent formatting in all of your configuration files. The terraform fmt command automatically updates configurations in the current directory for readability and consistency.

            $ terraform fmt

#You can also make sure your configuration is syntactically valid and internally consistent by using the terraform validate command.
        
    $ terraform validate

     Success! The configuration is valid.
	
	
#Apply the configuration now with the terraform apply command. Terraform will print output similar to what is shown below. We have truncated some of the output to save space.
	
                   $ terraform apply


                An execution plan has been generated and is shown below.
                Resource actions are indicated with the following symbols:
                  + create

                  Terraform will perform the following actions:

                  # aws_instance.app_server will be created
                  + resource "aws_instance" "app_server" {
                      + ami                          = "ami-830c94e3"
                      + arn                          = (known after apply)
                ##...

                Plan: 1 to add, 0 to change, 0 to destroy.

                Do you want to perform these actions?
                  Terraform will perform the actions described above.
                  Only 'yes' will be accepted to approve.

                 Enter a value: yes

                aws_instance.app_server: Creating...
                aws_instance.app_server: Still creating... [10s elapsed]
                aws_instance.app_server: Still creating... [20s elapsed]
                aws_instance.app_server: Still creating... [30s elapsed]
                aws_instance.app_server: Creation complete after 36s [id=i-01e03375ba238b384]

                Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

                #Inspect the current state using terraform show.

                $ terraform show

                 aws_instance.app_server:
                resource "aws_instance" "app_server" {
                    ami                          = "ami-830c94e3"
                    arn                          = "arn:aws:ec2:us-west-2:561656980159:instance/i-01e03375ba238b384"
                    associate_public_ip_address  = true
                    availability_zone            = "us-west-2c"
                    cpu_core_count               = 1
                    cpu_threads_per_core         = 1
                    disable_api_termination      = false
                    ebs_optimized                = false
                    get_password_data            = false
                    hibernation                  = false
                    id                           = "i-01e03375ba238b384"
                    instance_state               = "running"
	
	
#Terraform has a built-in command called terraform state for advanced state management. Use the list subcommand to list of the resources in your project's state.
	
	$ terraform state list
    aws_instance.app_server
    
#destroy all

        $terraform destroy
    
  # finish.........
