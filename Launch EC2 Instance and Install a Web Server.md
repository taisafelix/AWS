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

11. Add the www group to your EC2 instance
```javascript
[ec2-user ~]$ sudo groupadd www
```          
12. Add the ec2-user user to the www group
```javascript
[ec2-user ~]$ sudo usermod -a -G www ec2-user
```                 
13. Exit to refresh the previous modifications
```javascript
[ec2-user ~]$ exit
```  
14. Connect again to the EC2 instance and verify that the www group exists with the groups command.
```javascript
[ec2-user ~]$ groups
ec2-user wheel www
```  

15. Change the group ownership of the /var/www directory and its contents to the www group.
```javascript
[ec2-user ~]$ sudo chown -R root:www /var/www
```              

16. Change the directory permissions of /var/www and its subdirectories to add group write permissions and set the group ID on subdirectories created in the future.
```javascript
[ec2-user ~]$ sudo chmod 2775 /var/www
[ec2-user ~]$ find /var/www -type d -exec sudo chmod 2775 {} +
```             
17. Recursively change the permissions for files in the /var/www directory and its subdirectories to add group write permissions.
```javascript
[ec2-user ~]$ find /var/www -type f -exec sudo chmod 0664 {} +
```      
### Connect to Apache web server 

18. Change the directory to /var/www and create a new subdirectory named inc.
```javascript
[ec2-user ~]$ cd /var/www
[ec2-user ~]$ mkdir inc
[ec2-user ~]$ cd inc
``` 

19. Create a new file in the inc directory named dbinfo.inc, and then edit the file
```javascript
[ec2-user ~]$ >dbinfo.inc
[ec2-user ~]$ nano dbinfo.inc
``` 

20. Change the directory to /var/www/html.
```javascript
[ec2-user ~]$ cd /var/www/html
``` 
21. Create a new file in the html named SamplePage.php
```javascript
[ec2-user ~]$ >SamplePage.php
[ec2-user ~]$ nano SamplePage.php
```

22. Write your Hello code: 
```javascript
<html>
<head>
  <title>Hello</title>
 </head>
 <body>
 <?php echo '<p>Hello World</p>'; ?> 
 </body>
</html>
```
23. Save (Ctrl + X) and close the SamplePage.php file

24. **Et voilá!** Open a web browser and browse to:

http://ec2-your-instance.com/SamplePage.php

