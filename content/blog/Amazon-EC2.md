---
title: "Amazon EC2"
date: "2019-09-05"
draft: true
image: "imgs/blog-4.png"
description: "Steps to creating and setting up an Amazon EC2 instance."
tags: [
    "AWS", 
    "Linux", 
    "MySQL"
    ]
type: "post"
---

# How To Setup And Connect To An AWS EC2 instance.

## What is an EC2 instance?
Amazon Elastic Compute Cloud (Amazon EC2) provides scalable computing capacity in the Amazon Web Services (AWS) cloud. You can use Amazon EC2 to launch as many or as few virtual servers as you need, configure security and networking, and manage storage. It is basically a really quick and easy way to create a computer/virtual machine in the Amazon cloud.

## Log in or Create An Amazon Account

Log into your AWS account or create an account Amazon offers a really cool free tier package for the first year of your account so everthing being done here will be completely free.

Navigate to services and ec2 in the compute category
OR
go to ec2 dashboard:

  https://eu-west-2.console.aws.amazon.com/ec2/v2/home?region=eu-west-2#Home:

-------------------------------------------------------------------------------------------------------------

Click on the blue button "launch instance"

Go through the steps and select what you require to configure your virtual machine(VM):

- Choose and operating system to run on your instance. (I chose Ubuntu 18.04 so the following steps will require that OS.)
- Choose the instance type they vary in size and get given a family name (use case)
- Configure Instance Details ( number of instances, networking and behaviour settings )
- Add storage, (up to 30Gb for free tier)
- Add tags (name for key_pair)
- Configure Security Group, can make multiple per instance or use one on multiple instances
- Review to check all choices and then launch.
- When it asks for a private key file make a new one or use an existing one. (keep these safe,backup set as environment variable etc.)

Click view instances, this will return you to the dashboard where your instance will be instaniated and have a state, either "Running" or "Stopped".

-------------------------------------------------------------------------------------------------------------

You can now use/launch your instance it will take you to the terminal of the vm/instance, here you can install packages/progams like you would in Ubuntu Linux.

If we want to use MySQL we need to install it first:

    sudo apt update
    sudo apt install -y mysql-server mysql-client

Next we can use mysql to create our user which we will access the db remotely with.
sudo mysql

    CREATE USER 'my_username'@'%' IDENTIFIED BY 'my_password';

And then to grant permissions these are not a good idea for other users as it is all permissions allowed.

    GRANT ALL PRIVILEGES ON *.* TO 'my_username'@'%';

After this we can either create databases here with the cli or we can use a gui i.e Dbeaver.

The last thing would now be to allow remote connections to your instance.

Open port 3306 with a mysql rule in your security group on aws.

Open mysqld.cnf:

    sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

Remove the # tag to comment out the following line:
bind-address          = 127.0.0.1

Now restart the server.

    sudo service mysql restart

-------------------------------------------------------------------------------------------------------------

# TO CONNECT TO THE VM WITH LINUX
Make sure you select a working instance, and at the top click connect.

Open terminal, and change directory to the where your private key is (if you created a new one it will name the one needed)

Then run:

    chmod 400 private-key-name.pem

and now we can connect with ssh like so:

    ssh -i "private-key-name.pem" ubuntu@ec2-18-130-188-129.eu-west-2.compute.amazonaws.com <- this will be the public DNS

the ubuntu@ will be the operating system you selected and the public dns you can copy this from the field in the dashboard.
