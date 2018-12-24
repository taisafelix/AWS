## Easiest way: 
* EC2 Dashboard -> Instances Launch Instance
* Go to communities AMI -> Select Ubuntu and look for RStudio in the search box
* Select one of the machines > Review and Launch

## Easy way:
* Create a EC2 Linux instance
* In the prompt: 
  * sudo amazon-linux-extras install epel
  * sudo yum install R

## Difficult way:
* Create a VPC
* Create a public subnet inside the VCP you created
* Create an Internet Gateway and attatch it to your VPC 
* Create a Route Table and add the configuration: 
* Route Table -> Routes -> Edit -> Add 0.0.0.0/0 -> The target is the Internet Gateway you just created 
* Associate the route table to the VPC, to the Public Subnet and the Internet Gateway 
* Launch Instance -> In the Prompt:
  * sudo amazon-linux-extras install epel
  * sudo yum install R
