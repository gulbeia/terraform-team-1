# Terraform project: Team-1 - AWS

# Setup input parameters

Before building project set input variables!

* copy them to ~/.bashrc and reopen your terminal
* OR run them in CLI before run terraform command

They look like:
```
export TF_VAR_region=us-west-1
export PKR_VAR_region=$TF_VAR_region
export TF_VAR_domain_name=budaichiev.com
```

# To build Project

Run command
```
bash build.sh
```
# To destroy project

Run command:
```
bash destroy.sh
```


## VPC group:

Module is published at Terraform Registry (https://registry.terraform.io/modules/rus777777/vpc-t1/aws/latest) :
```
module "vpc-t1" {
  source  = "rus777777/vpc-t1/aws"
  ...
}
```

Source code is in the
```
git@github.com:rus777777/terraform-aws-vpc-t1.git
```
Members of VPC group can change it.


### Tasks (draft):

* Create some parameters to enable DNS (type bool) in vpc (enableDnsHostnames and enableDnsSupport) and subnets, it could be need for internal DB - negotiate with RDS group. Each parameter sets as input variable. Default value set as for default VPC.
* Create parameter (input variable, type bool) to create NAT gateway for each privite subnets.
* Add comments, description
* Refactoring (optimize) code if you want

- - -

## ASG group:

### Tasks (draft):

* Define what input parameters need from VPC. You can fetch them from VPC backend located in S3.
* Define what input parameters need from RDS. Fetch them from RDS backend or by RDS name?
* Undestand how wordpress works
* Undestand how to script installation wordpress with template
* Parker makes Golden Image

- - -
## RDS group:

Not finished yet.

Added some draft code to launch RDS:

* Not linked with our VPC
* Login/Password is stored in Parameter Store.
* RDS resides in public subnets to be accessible from Internet - easy to check.
* Security Group is allow to access from Internet to port 3306


### Tasks (draft):
* Define what input parameters need from VPC. You can fetch them from VPC backend located in S3.
* Is RDS locate in private subnets?
* In <writer/reader>.yourdomain.com: is <yourdomain.com> internal domain?
* Negotiate with VPC group about certain parameters of VPC (enableDnsHostnames and enableDnsSupport) and subnet to enable DNS
* If RDS resides in private subnets, it could only accessable through the bastion host.
* [bonus] how to create DB in RDS, create/select table, fill table by script?

- - -

# Helpful links:

Markdown Cheatsheet

https://github.com/tchapi/markdown-cheatsheet/blob/master/README.md


Reference architecture

https://docs.aws.amazon.com/whitepapers/latest/best-practices-wordpress/reference-architecture.html

- - -

- - - 

# Project 

Project description

# Project goals (1 page)

* Project tasks:
  * create infrustructure architecture 
  * the size of the resources (could be parameterized)
  * determine dependencies between groups 
  * flexibility of the code
  * make regionless dependency
    * deploy into another region with a few clicks
    * resources should not depend on specific region

* Team communication:
  * How to negotatate with groups inside team
    * chat channel (telegram)
    * zoom
    * etc
  * which backends we use

# Org structure (1 page)

Members of:
* VPC group
* RDS group
* ASG group

# Infrastructure architecture (1 page)

* Current infrastructure of our Project -  Anelia will share later

* create primitive model (prototype) of our project to negotiate beetwen groups

# VPC (1-3 pages)

* make base for other groups - RDS, ASG should not wait
* VPC organise as a Terraform mudule
* module published in Terraform Registry for public use

VPC
* 3 public subnets
* 3 private subnets
* 1 GW
* (depend on parameter) NAT GW 

# RDS (1-3 pages)

* RDS instanse -  for simple model - ASG should not wait
* using resources Aurora cluster
* publish in Route53:
  * writer.yourdomain.com
  * reader1.yourdomain.com
  * reader2.yourdomain.com
  * reader3.yourdomain.com

# ASG (1-3 pages)

* depend on VPC, RDS groups
* Packer - for making golden image for ASG
  * not depend on region
  * not depend on AWS account
* ASG template - automaticale choose latest golden image
  * use templatefile() for dynamic create file with needed parameters
* userdata
  * automative script to startup Wordpress and connect to DB

* wordpress is accessable through ALB by address <b>wordpress.yourdomain.com</b>

# Outputs / resume (1 page)

* we successfully made this project
  * flexibility of the code 
  * deploy into another region with a few clicks
  * expirience 3-tire architecture
  * undestood every stage of the project, correlation between groups 
  
* what we learn from this project 

* how many time (hours) team members contribute to project
