# Getting Started with Terraform in AWS

## Prerequisites

* Internet connection
* An AWS account
* Your AWS credentials 
* AWS CLI installed
* AWS Provider configured (See [Terraform AWS Docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs))

## Get the tutorial for you
Terraform is a tool that allows you to build, change, and version infrastructure as code. 
Terraform helps you manage cloud infrastructure with configuration files instead of a graphical user interface (GUI).  
We provide Getting Started Guides for [AWS](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started),  [OCI](https://learn.hashicorp.com/collections/terraform/oci-get-started), [GCP](https://learn.hashicorp.com/collections/terraform/gcp-get-started), [Docker](https://learn.hashicorp.com/collections/terraform/docker-get-started), and [Azure](https://learn.hashicorp.com/collections/terraform/azure-get-started).

## Install Terraform

Go to [Terraform.io](https://www.terraform.io/downloads.html) and download the installation file. 
Run the executable file in your environment. 


### Verify the installation
```shell
$ terraform-help
```
Output shows Terraform subcommands when installation is working.

### Create Directory
Create a directory for the Terraform configuration file.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```
### Create Configuration
Create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Copy the text below and Paste it into the file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```
This code configures a docker container with the latest Nginx image. 

### Initialize Terraform

Initialize Terraform with the `init` command and the AWS provider will be installed. 

```shell
$ terraform init
```

Note: If you see errors in the output check that you have all the [Prerequisites] (https://github.com/13903282022/hcorp2/blob/main/terraform-getting-started.md#prerequisites) listed at the top of this document. 

### Build resources

```shell
$ terraform apply
```

The command may take a few minutes to run and when done output shows the resources are created.

### Destroy resources
Next you destroy the infrastructure.

```shell
$ terraform destroy
```

When the shell asks for confirmation type `yes` and hit ENTER. 

Terraform destroys the resources created earlier.

# Next Steps
Go to https://learn.hashicorp.com/terraform to view more Terraform tutorials.



