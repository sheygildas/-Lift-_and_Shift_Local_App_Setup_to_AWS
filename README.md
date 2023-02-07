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
<br/>

### :bulb: Launch Instances with user data 

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :earth_africa: Update IP to name mapping in route 53

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
