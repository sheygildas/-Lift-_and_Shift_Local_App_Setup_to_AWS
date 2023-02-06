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
- A tool
- B tool

| Name | Description |
| --- | --- |
| [`@toast-ui/editor-plugin-chart`](https://github.com/nhn/tui.editor/tree/master/plugins/chart) | Plugin to render chart |
| [`@toast-ui/editor-plugin-code-syntax-highlight`](https://github.com/nhn/tui.editor/tree/master/plugins/code-syntax-highlight) | Plugin to highlight code syntax |
| [`@toast-ui/editor-plugin-color-syntax`](https://github.com/nhn/tui.editor/tree/master/plugins/color-syntax) | Plugin to color editing text |
| [`@toast-ui/editor-plugin-table-merged-cell`](https://github.com/nhn/tui.editor/tree/master/plugins/table-merged-cell) | Plugin to merge table columns |
| [`@toast-ui/editor-plugin-uml`](https://github.com/nhn/tui.editor/tree/master/plugins/uml) | Plugin to render UML 

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

## :cloud: AWS Services

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
</div>
<br/>

### :closed_lock_with_key: Create Key Pairs

<br/>
<div align="right">
    <b><a href="#Project-03">↥ back to top</a></b>
</div>
<br/>

### :lock: Create Security groups

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
