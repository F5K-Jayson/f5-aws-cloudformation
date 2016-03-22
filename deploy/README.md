
# DEPLOY

Although these Cloudformation templates are meant to serve more as a reference, you can indeed deploy them directly.  

The templates prefixed with "existing-stack" are generally more indicative of how we expect customers to deploy Big-IPs (insertion into an existing environment).

However, we include templates (prefixed with "full-stack") that setup an full sample enviornment (VPC, subnets, security groups, sample webserver, etc.) that you can quickly have a working deployment to explore.  

## Example of deploying stacks through aws cli:


###1 NIC:


####Full Stack - BYOL:

    aws cloudformation create-stack 
    --region us-west-2 
    --template-body file://full-stack-vpc-w-byol-1nic-bigip.template 
    --stack-name full-stack-bigip-1nic
    --parameters  
    ParameterKey=KeyName,ParameterValue=YOUR-SSH-KEY
    ParameterKey=AvailabilityZone1,ParameterValue=us-west-2a
    ParameterKey=AvailabilityZone2,ParameterValue=us-west-2b
    ParameterKey=BigipInstanceType,ParameterValue=m3.xlarge
    ParameterKey=BigipPerformanceType,ParameterValue=Good
    ParameterKey=WebserverInstanceType,ParameterValue=t1.micro
    ParameterKey=BigipAdminUsername,ParameterValue=admin
    ParameterKey=BigipAdminPassword,ParameterValue='YOURPASSWORD'
    ParameterKey=BigipManagementGuiPort,ParameterValue=443
    ParameterKey=BigipLicenseKey,ParameterValue=LUFJD-YREAG-VQHVI-EYOQH-JBBKXAI

####Existing Stack - BYOL:

    aws cloudformation create-stack 
    --region us-west-2 
    --template-body file://existing-stack-byol-1nic-bigip.template
    --stack-name existing-stack-bigip-1nic
    --parameters  
    ParameterKey=KeyName,ParameterValue=YOUR-SSH-KEY
    ParameterKey=BigipInstanceType,ParameterValue=m3.xlarge
    ParameterKey=BigipPerformanceType,ParameterValue=Good
    ParameterKey=BigipAdminUsername,ParameterValue=admin
    ParameterKey=BigipAdminPassword,ParameterValue='YOURPASSWORD'
    ParameterKey=BigipManagementGuiPort,ParameterValue=443
    ParameterKey=Vpc,ParameterValue=vpc-61a94705
    ParameterKey=Az1ExternalSubnet,ParameterValue=subnet-aec1d4d9
    ParameterKey=BigipExternalSecurityGroup,ParameterValue=sg-d90eb9be
    ParameterKey=WebserverPrivateIp,ParameterValue="10.0.3.8"
    ParameterKey=DnsServers,ParameterValue="10.0.0.2"
    ParameterKey=BigipLicenseKey,ParameterValue=NEHQF-CDKUY-RJTJB-XSPTZ-XVKSQJS


####Existing Stack - BIG-IQ License Pool:

    aws cloudformation create-stack 
    --region us-west-2 
    --template-body file://existing-stack-bigiq-license-pool-1nic-bigip.template
    --stack-name existing-stack-bigiq-license-pool-bigip-1nic
    --parameters  
    ParameterKey=KeyName,ParameterValue=YOUR-SSH-KEY
    ParameterKey=BigipInstanceType,ParameterValue=m3.xlarge
    ParameterKey=BigipPerformanceType,ParameterValue=Good
    ParameterKey=BigipAdminUsername,ParameterValue=admin
    ParameterKey=BigipAdminPassword,ParameterValue='YOURPASSWORD'
    ParameterKey=BigipManagementGuiPort,ParameterValue=443
    ParameterKey=Vpc,ParameterValue=vpc-61a94705
    ParameterKey=Az1ExternalSubnet,ParameterValue=subnet-aec1d4d9
    ParameterKey=BigipExternalSecurityGroup,ParameterValue=sg-d90eb9be
    ParameterKey=WebserverPrivateIp,ParameterValue="10.0.3.8"
    ParameterKey=DnsServers,ParameterValue="10.0.0.2"
    ParameterKey=BigiqUsername,ParameterValue=admin 
    ParameterKey=BigiqPassword,ParameterValue='YOURPASSWORD' 
    ParameterKey=BigiqAddress,ParameterValue=52.89.223.222 
    ParameterKey=BigiqLicensePoolUUID,ParameterValue=5ba3f9b1-52f1-4fd1-93fd-111111b5aa23


###2 NIC:

####Full Stack:

    aws cloudformation create-stack 
    --region us-west-2 
    --template-body file://full-stack-vpc-w-byol-2nic-bigip.template 
    --stack-name full-stack-bigip-2nic
    --parameters  
    ParameterKey=KeyName,ParameterValue=YOUR-SSH-KEY
    ParameterKey=AvailabilityZone1,ParameterValue=us-west-2a
    ParameterKey=AvailabilityZone2,ParameterValue=us-west-2b
    ParameterKey=BigipInstanceType,ParameterValue=m3.xlarge
    ParameterKey=BigipPerformanceType,ParameterValue=Good
    ParameterKey=WebserverInstanceType,ParameterValue=t1.micro
    ParameterKey=BigipAdminUsername,ParameterValue=admin
    ParameterKey=BigipAdminPassword,ParameterValue='YOURPASSWORD'
    ParameterKey=BigipLicenseKey,ParameterValue=HOXXC-QTDPU-KARFZ-GCNAN-EKVPEDU

####Existing Stack:

    aws cloudformation create-stack 
    --region us-west-2 
    --template-body file://existing-stack-byol-2nic-bigip.template
    --stack-name existing-stack-bigip-2nic
    --parameters  
    ParameterKey=KeyName,ParameterValue=YOUR-SSH-KEY
    ParameterKey=BigipInstanceType,ParameterValue=m3.xlarge
    ParameterKey=BigipPerformanceType,ParameterValue=Good
    ParameterKey=BigipAdminUsername,ParameterValue=admin
    ParameterKey=BigipAdminPassword,ParameterValue='YOURPASSWORD'
    ParameterKey=Vpc,ParameterValue=vpc-8a05ebee
    ParameterKey=Az1ExternalSubnet,ParameterValue=subnet-436d7934
    ParameterKey=Az1ManagementSubnet,ParameterValue=subnet-406d7937
    ParameterKey=BigipExternalSecurityGroup,ParameterValue=sg-bd8c3dda
    ParameterKey=BigipManagementSecurityGroup,ParameterValue=sg-bc8c3ddb
    ParameterKey=WebserverPrivateIp,ParameterValue="10.0.3.39"
    ParameterKey=DnsServers,ParameterValue="10.0.0.2"
    ParameterKey=BigipLicenseKey,ParameterValue=CCSVQ-ZXHDA-JBJYU-ZKXZI-LLUHUMX


## deploy_stacks.py

As a further convience, we have included a simple python script (deploy_stacks.py) that can string together the two related "full" and "existing" tempates

ex.

    python deploy_stacks.py -t full-stack-vpc-w-byol-1nic-bigip.template,existing-stack-byol-1nic-bigip.template -r TEQNR-OUBKH-YGRLC-ISTMV-WCBNYGN,WRZUG-PSFAF-DFRBR-AXAIP-GEZDDTC

This will launch the first full stack (vpc, subnets, security groups, bigip, webserver) and use the various outputs (vpc, subnets, security groups, etc.) for creating the next stack (bigip-only in an existing stack).  

#####Known Issues:


1. Some Full stack templates may get too large to be deployed via AWS cli.

		'templateBody' failed to satisfy constraint: Member must have length less than or equal to 51200

   **Workaround:** _Use AWS console, store template on S3, or minify_




