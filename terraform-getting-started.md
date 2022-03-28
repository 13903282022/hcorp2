# Getting Started with Terraform

Terraform is a tool that allows you to build, change, and version infrastructure safely and efficiently.  

## Install Terraform

Go to [Terraform.io](https://www.terraform.io/downloads.html) and download the installation file for your environment.

### Create Terraform Directory
Create a directory for the Terraform configuration file.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```
## Create Terraform Configuration File
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

### Initialize Terraform

Initialize Terraform with the `init` command and the AWS provider will be installed. 

```shell
$ terraform init
```
## Check for Errors
You shoud check for any errors before moving on to the next step. 

### Provision resources with `apply` 

```shell
$ terraform apply
```

The command may take a few minutes to run. When complete you will see a message that the resources are created.

### Remove resources with `destroy`
Next you destroy the infrastructure.

```shell
$ terraform destroy
```

When the output asks for confirmation type `yes` and hit ENTER. 

Terraform destroys the resources created earlier.

# Next Steps
Go to https://learn.hashicorp.com/terraform to see all the Terraform tutorials.


