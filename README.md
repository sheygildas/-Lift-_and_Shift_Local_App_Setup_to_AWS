# Project-03
# Lift and Shift Local App Setup to AWS Cloud
## :ledger: Index

- [About The Project](#beginner-about-the-project)
- [Problem that this project solves ](#question-problem-that-this-project-solves)
- [Solution to the problem.](#key-solution-to-the-problem)
- [Prerequisites](#hammer_and_wrench-prerequisites)
- [AWS Services](#cloud-aws-services)
- [Architecture of this project](#house-architecture-of-this-project)
- [Steps to execute the project](#zap-steps-to-execute-the-project)
  - [Login to AWS Account ](#key-login-to-aws-account )
  - [Create Key Pairs](#closed_lock_with_key-create-key-pairs)
  - [Create Security groups](#lock-create-security-groups)
  - [Launch Instances with user data](#bulb-launch-instances-with-user-data )
  - [Update IP to name mapping in route 53](#earth_africa-update-ip-to-name-mapping-in-route-53)
  - [Build Application from source code](#hammer_and_wrench-build-application-from-source-code)
  - [Upload to S3 bucket](#rocket-upload-to-S3-bucket)
  - [Download artifact to Tomcat Ec2 Instance](#package-download-artifact-to-tomcat-ec2-instance)
  - [Setup ELB with HTTPS ](#lock-setup-elb-with-https )
  - [Map ELB Endpoint to website name in DNS](#earth_africa-map-elb-endpoint-to-website-name-in-dns)
  - [Build Autoscaling Group for Tomcat Instances](#hammer_and_wrench-build-autoscaling-group-for-tomcat-nstances)
- [Verify from browser](#earth_africa-verify-from-browser) 
- [Resources](#page_facing_up-resources)
- [Credit/Acknowledgment](#star2-creditacknowledgment)


## :beginner:About The Project

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

## :question: Problem that this project solves 

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

## :key: Solution to the problem.

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

## :hammer_and_wrench: Prerequisites

- visual studio code
- AWS Account
- AWS CLI
- Maven
- Registered DNS Name
- JDK8

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

## :cloud: AWS Services
- EC2 instance
- ELB
- Autoscalling
- S3
- EFS
- Route 53
- 

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

## :beginner: Architecture of this project.

![Project Image](project-image-url)

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

## :zap: Steps to Execute the project. 

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :key: Login to AWS Account

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>`
<br/>

### :closed_lock_with_key: Create Key Pairs

- Now that yu are login let's create a Keypair to connect our EC2 instances through SSH.

![Project Image](project-image-url)

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :lock: Create Security groups

- Let's start by creating security group for the load-balancer and name it "vprofile-ELB-SG'. 
- Set 'inbound rules' to allow 'HTTP' on port '80' and 'HTTPS' on port 443 from Anywhere

![Project Image](project-image-url)

- Create another security group for our application and name it 'vprofile-app-SG'. 
- Set 'inbound rules' to allow port '8080' to accept traffic from from the load-balancer security group 'vprofile-ELb-SG'.



![Project Image](project-image-url)


- Lastly, create a security group for the backend services and name it 'vprofile-backend-SG'. 
- Set 'inbound rules' to allow  11211 for Memcached, 5672 for RabbitMQ and port 3306 for MySQL server.
- Note: application.properties file found under [src/main/resources](https://github.com/sheygildas/Local_App_Setup/tree/local-setup/src/main/resources) directory, contain all the port rhat have to be open for our application services to communicate each other. 
- Allow all traffic from backends' own security group so that the backend services can communicate with each other.


![Project Image](project-image-url)


<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>

### :bulb: Launch Instances with user data 

- Note: Launching  Instances with user data  may take some time. If you SSH into the server and the user data is not yet provision, you can check the process 'ps -ef' to see if the process to provision user data has started or failed. If the process has started, wait for sometime and check with 'systemctl status' '<service_name>' command again.

#### Provision DB Instance

- We will start by creating DB instance with details as given below. The user data script is found at this [location](https://github.com/sheygildas/Local_App_Setup/blob/local-setup/vagrant/Automated_provisioning/mysql.sh)
- We also have to add 'inbound rule' to 'vprofile-backend-SG' which is our backend SG to ALLOW SSH on port 22 from My IP to be able to connect our db instance.

 ```sh
Name of Instance: vprofile-db01
Project: vprofile
AMI: Centos 7
InstanceType: t2.micro
SecGrp: vprofile-backend-SG
UserData: mysql.sh
   ```
   
- Let't launch our EC2 instance using the above userdata.
   
![Project Image](project-image-url)

- When the instance is up and running, SSH into the server and check if userdata script is executed. If everything is ok proceed to check the status of mariadb.

```sh
ssh -i vprofile-prod-key.pem centos@<public_ip_of_instance>
sudo su -
curl http://169.254.169.254/latest/user-data
systemctl status mariadb
   ```

![Project Image](project-image-url)

#### Provision Memcached Instance

- We will start by creating memcached instance with details as given below.

```sh
Name of Instance : vprofile-mc01
Project: vprofile
AMI: Centos 7
InstanceType: t2.micro
SecGrp: vprofile-backend-SG
UserData: memcache.sh
   ```
- - Let't launch our EC2 instance using the above userdata. The user data script is found at this [location](https://github.com/sheygildas/Local_App_Setup/blob/local-setup/vagrant/Automated_provisioning/memcache.sh)

![Project Image](project-image-url)

- When the instance is up and running, SSH into the server and check if userdata script is executed. If everything is ok proceed to check the status of memcached.
 
```sh
ssh -i vprofile-prod-key.pem centos@<public_ip_of_instance>
sudo su -
curl http://169.254.169.254/latest/user-data
systemctl status memcached.service
ss -tunpl | grep 11211
   ```

![Project Image](project-image-url)


#### Provision RabbitMQ Instance

- We will start by creating RabbitMQ instance with details as given below. The user data script is found at this [location](https://github.com/sheygildas/Local_App_Setup/blob/local-setup/vagrant/Automated_provisioning/rabbitmq.sh)
 
 ```sh
Name of Instance: vprofile-rmq01
Project: vprofile
AMI: Centos 7
InstanceType: t2.micro
SecGrp: vprofile-backend-SG
UserData: rabbitmq.sh
   ```
- When the instance is up and running, SSH into the server and check if userdata script is executed. If everything is ok proceed to check the status of rabbitmq

 ```sh
ssh -i vprofile-prod-key.pem centos@<public_ip_of_instance>
sudo su -
curl http://169.254.169.254/latest/user-data
systemctl status rabbitmq-server
   ```
   
![Project Image](project-image-url)

#### Provision Application Instance

- We will start by creating Application instance with details as given below. The user data script is found at this [location](https://github.com/sheygildas/Local_App_Setup/blob/local-setup/vagrant/Automated_provisioning/tomcat_ubuntu.sh)
 
 
 ```sh
Name: vprofile-app01
Project: vprofile
AMI: Ubuntu 18.04
InstanceType: t2.micro
SecGrp: vprofile-app-SG
UserData: tomcat_ubuntu.sh
   ```
- Add Inbound rule to 'vprofile-app-SG' for SSH on port 22 from My IP to be able to connect our db instance via SSH.

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :earth_africa: Update IP to name mapping in route 53

- Now that our Backend instances are up and running, it time to update the private IP of our backend services in Route53 Private DNS Zone
- Check the private IP address of your instances and update them in Route 53.


![Project Image](project-image-url)

- Create a Private Hosted zone in Route53 and name it "vprofile.in'.

![Project Image](project-image-url)

- Create records for our backend services and add the record names in our application.properties file found in this location [location](https://github.com/sheygildas/Local_App_Setup/blob/local-setup/vagrant/Automated_provisioning/application.properties).
 
 ![Project Image](project-image-url)


<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :hammer_and_wrench: Build Application from source code



<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :rocket: Upload to S3 bucket

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :package: Download artifact to Tomcat Ec2 Instance

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :lock: Setup ELB with HTTPS 

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :earth_africa: Map ELB Endpoint to website name in DNS

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :hammer_and_wrench: Build Autoscaling Group for Tomcat Instances

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

## :earth_africa: Verify from browser

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>


## :page_facing_up: Resources

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>


## :star2: Acknowledgment


<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>
