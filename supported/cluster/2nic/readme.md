# Deploying the BIG-IP in AWS - 2 NIC

[![Slack Status](https://f5cloudsolutions.herokuapp.com/badge.svg)](https://f5cloudsolutions.herokuapp.com)
[![Doc Status](http://readthedocs.org/projects/f5-sdk/badge/?version=latest)](https://support.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/bigip-ve-multi-nic-setup-amazon-ec2-12-1-0.html)

## Introduction

This solution implements a Cloud Formation Template to deploy a base example of F5 in a clustered, highly available configuration across availability zones using a two NIC deployment. In a two NIC implementation, interface #1 is for management and data-plane traffic from the Internet, and interface #2 is connected into the Amazon networks where traffic is processed by the pool members in a traditional two-ARM design. 

This template deploys and configures two BIG-IPs in a clustered configuration across specified availability zones. The F5 solution provides two different template options:
  - **BYOL**<br>
  The BYOL (bring your own license) template allows you to input an existing BIG-IP license.
  - **Hourly**<br>
  The Hourly template which uses pay-as-you-go hourly billing
  
The **existing stack** CloudFormation template incorporates an existing Virtual Private Cloud (VPC). If you would like to run a *full stack* which creates and configures the BIG-IP, the AWS infrastructure, as well as a backend webserver, see the templates located in the **learning-stacks** folder.
  
## Documentation

The ***BIG-IP Virtual Edition and Amazon Web Services: Multi-NIC Setup*** guide (https://support.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/bigip-ve-multi-nic-setup-amazon-ec2-12-1-0.html) decribes how to create the configuration manually without using the CloudFormation template.


## Installation

You have two options for deploying this template: 
  - Using the AWS deploy buttons 
  - Using [CLI Tools](#cli)

### Using the AWS deploy buttons
The easiest way to deploy of the of CloudFormation templates is to use the appropriate Launch button below.

**Hourly deploy button**

Use this button to deploy the **hourly** template: 

<a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=BigIp-Across-Az-Cluster-2nic-Hourly&templateURL=https://s3.amazonaws.com/f5-cft/f5-existing-stack-across-az-cluster-hourly-2nic-bigip.template">
    <img src="https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png"/>
</a>
<br>
<br>

After clicking the Launch button, you must specify the following parameters.
<br>

| Parameter | Required | Description |
| --- | --- | --- |
| adminPassword | x | Type the BIG-IP admin password |
| adminUsername | x | Type the BIG_IP user name |
| bigipExternalSecurityGroup | x | Public or External Security Group ID |
| bigipManagementSecurityGroup | x | BIG-IP Management Security Group ID |
| imageName | x | F5 BIG-IP Performance Type |
| instanceType | x | BIG-IP virtual instance type |
| managementSubnetAz1 | x | Management subnet ID |
| restrictedSrcAddress | x | The IP address range that can be used to SSH to the EC2 instances |
| sshKey | x | Name of an existing EC2 KeyPair to enable SSH acccess to the instance |
| subnet1Az1 | x | Public or External subnet ID |
| Vpc | x | Common VPC for the deployment |
| webserverPrivateIp | x | Web Server IP used for the BIG-IP pool member |


<br>
<br>
  **BYOL deploy button**

Use this button to deploy the **BYOL** template: 

<a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=BigIp-Across-Az-Cluster-2nic-byol&templateURL=https://s3.amazonaws.com/f5-cft/f5-existing-stack-across-az-cluster-byol-2nic-bigip.template">
    <img src="https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png"/>
</a>

<br>
After clicking the Launch button, you must specify the following parameters.

| Parameter | Required | Description |
| --- | --- | --- |
| adminPassword | x | Type the BIG-IP admin password |
| adminUsername | x | Type the BIG_IP user name |
| bigipExternalSecurityGroup | x | Public or External Security Group ID |
| bigipManagementSecurityGroup | x | BIG-IP Management Security Group ID |
| iamAccessKey | x | Type the IAM Access Key |
| iamSecretKey | x | Type the IAM Secret Key for BIG-IP |
| imageName | x | F5 BIG-IP Performance Type |
| instanceType | x | BIG-IP virtual instance type |
| licenseKey1 | x | Type or paste your F5 BYOL regkey here |
| licenseKey2 | x | Type or paste your F5 BYOL regkey here |
| managementSubnetAz1 | x | Management subnet ID |
| managementSubnetAz2 | x | Management subnet ID |
| restrictedSrcAddress | x | The IP address range that can be used to SSH to the EC2 instances |
| sshKey | x | Name of an existing EC2 KeyPair to enable SSH acccess to the instance |
| subnet1Az1 | x | Public or External subnet ID |
| subnet1Az2 | x | Public or External subnet ID |
| Vpc | x | Common VPC for the deployment |
| webserverPrivateIp | x | Web Server IP used for the BIG-IP pool member |




### <a name="cli"></a>AWS CLI Usage
Coming soon

## Design Patterns


The goal is for the design patterns for all the iterative examples of F5 being deployed via ARM templates to closely match as much as possible.

### List of Patterns For Contributing Developers


 1. Still working on patterns to use

## Filing Issues

See the Issues section of `Contributing <CONTRIBUTING.md>`__.

## Contributing

See `Contributing <CONTRIBUTING.md>`__

## Test


Before you open a pull request, your code must have passed a deployment into Azure with the intended result

## Unit Tests

Simply deploying the ARM template and completing use case fulfills a functional test



## Copyright

Copyright 2014-2016 F5 Networks Inc.


## License


Apache V2.0
~~~~~~~~~~~
Licensed under the Apache License, Version 2.0 (the "License"); you may not use
this file except in compliance with the License. You may obtain a copy of the
License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations
under the License.

Contributor License Agreement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Individuals or business entities who contribute to this project must have
completed and submitted the `F5 Contributor License Agreement`