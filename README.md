# AWS101 Study Case

http://3.18.107.185

Final project appearance;

![case1](https://user-images.githubusercontent.com/77046207/116318236-21a43800-a7bd-11eb-9159-290bbdbde2e6.png)

# Steps

1. I created an IAM user to avoid any permanent changes on root account. I gave Administrator Access option to this user then connected this IAM user.

![case2](https://user-images.githubusercontent.com/77046207/116318690-d6d6f000-a7bd-11eb-97e2-8ef41648d859.png)

2. Launched an intance, but in building step I had used "User Data" option. This means that we won't go for installation of content of user data when we first open virtual machine. In the end my virtual machine contains Apache, PHP, Wordpress.


![case9](https://user-images.githubusercontent.com/77046207/116319855-e9522900-a7bf-11eb-8ae5-94badb26fe64.png)


3. I went RDS (Relational Database Service) section and created database according to case requirements. While
doing this step, I followed this path: Security Group > EC2 Security Group - Inbound (consider Inbound option) > Edit inbound rules > Select running instance.
This path provide us that our instance will be able to access database itself.

![case8](https://user-images.githubusercontent.com/77046207/116318897-3503d300-a7be-11eb-8830-bfc018718720.png)

4. Open virtual machine and check unless user data commands work. After that go into MySQL section to introduce your RDS database to your machine. In this section
I followed some queries like "CREATE USER, CREATE DATABASE, GRANT ALL PRIVILEGES ON, FLUSH PRIVILEGES". In the next step we are going to edit wp-config.php file. This wp files comes from installation of WordPress which occured at launching of instance. WordPress site can not be established without database.

![case10](https://user-images.githubusercontent.com/77046207/116320404-db50d800-a7c0-11eb-8e22-65a84c2da006.png)

5. We got data which provide us to introduce our RDS database to our machine. We are about to edit wp-config.php file to confirm this.
After this edit process, < cp -r wordpress/* /var/www/html/ > applied this due to access directly to WordPress site (such like 0.0.0.0) then I deleted wordpress folder 
in case confliction. After all these I had done one more change. Opened the httpd.conf file ( /etc/httpd/conf/httpd.conf ) and below  <Directory "/var/www/html">. section, I had changed the AllowOverride None line in the above section to read AllowOverride All.

![case11](https://user-images.githubusercontent.com/77046207/116321691-3257ac80-a7c3-11eb-81af-6bffeec54d21.png)

6. I gave permissions to the Apache server by using these commands

     >sudo chown -R apache /var/www
     >sudo chgrp -R apache /var/www
     >sudo chmod 2775 /var/www
     >find /var/www -type d -exec sudo chmod 2775 {} \;
     >find /var/www -type f -exec sudo chmod 0664 {} \;

7. After restarting my Apache server (systemctl restart httpd) I can access my WordPress site as mentioned on top.

8. I created a S3 Bucket for creating some WordPress back up service. S3 Bucket provides us this kind of opportunity. For applying this we use some aws configure commands.

![case3](https://user-images.githubusercontent.com/77046207/116323860-92e8e880-a7c7-11eb-9e64-debfa414d072.png)




![case12](https://user-images.githubusercontent.com/77046207/116322524-ec9be380-a7c4-11eb-9b04-8f9e3629ba39.png)

![case13](https://user-images.githubusercontent.com/77046207/116324304-9335b380-a7c8-11eb-9e67-38d41973698a.png)

9) Now I go for CloudWatch;

![case14](https://user-images.githubusercontent.com/77046207/116324540-04756680-a7c9-11eb-8c53-3db9c1d7959b.png)

![case5](https://user-images.githubusercontent.com/77046207/116324596-1951fa00-a7c9-11eb-8e3f-9fb039b78e53.png)

![case7](https://user-images.githubusercontent.com/77046207/116324666-338bd800-a7c9-11eb-964c-cc3464b3478b.png)









