### Task: Create a Webpage with Hello on it: 


1. Create your VPC
   - Services -> VPC -> Launch VPC Wizard -> VPC with Public and Private Subnets

3. Create a Route Table 
	- Routes -> Edit Routes -> Add route -> 0.0.0.0/0. Choose the internet gateway you just created 
	- Go to Subnet Asoociation -> Edit -> choose the right subnet

4. Create a Security Group
   * Configurations rules:
      * HTTP 80 - Anywhere
      * SSH 22 - Anywhere

5. Launch an EC2 Amazon Linux Instance
   * Configurations
      * Network: Choose the VPC you just created
      * Subnet: Choose an existing public subnet
      * Auto-assign Public IP: Enable.
      * Security Group: Select the security group you created in step number **4**
      
### Install an Apache Web Server with PHP

6. Connect to the EC2 instance that you created

7. Update the software on your EC2 instance:

```javascript 
[ec2-user ~]$ sudo yum update -y   // -y is to install the updates without asking for confirmation
```

8. Install the Apache web server with the PHP software package
```javascript
[ec2-user ~]$ sudo yum install -y httpd php
```           

9. Start the web server 
```javascript
[ec2-user ~]$ sudo service httpd start
```            

10. Configure the web server to start with each system boot using the chkconfig command.
```javascript
[ec2-user ~]$ sudo chkconfig httpd on
```                 
