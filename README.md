# FaultTolerantHPCConAWS

Besides this README.md file, this repository contains only one file, FaultTolerantHPCConAWS.json, which is a CloudFormation template that launches a fault tolerant HPCC cluster.

FaultTolerantHPCConAWS.json has similar functionality as the CloudFormation template and scripts in the repository, https://github.com/tlhumphrey2/EasyFastHPCCoAWS.

The new functionality in FaultTolerantHPCConAWS.json is that it creates a fault tolerant HPCC System. That is, if an instance of the cluster goes down, a new instance is launched to replace it and the EBS volume attached to the downed instance is attached to the replacement instance.

Also, FaultTolerantHPCConAWS.json is easier to use. With it, you no longer have to create an s3 bucket and load it with a private key and the scripts in https://github.com/tlhumphrey2/EasyFastHPCCoAWS/AWSInstanceFiles.


## How to Use FaultTolerantHPCConAWS.json

1. Load FaultTolerantHPCConAWS.json into CloudFormation.
2. Select a unique stack name (one you have never used and doesn't currently exist).
3. Set the parameters of your HPCC System and the parameters needed by AWS to launch your cluster. 
4. Be sure to enter an email address that works and that you can access. The launch process will send information to this email (like the ssh private key and the ECL Watch IP address). Also, when the cluster is ready, the launch process will let you know via email or if a instance goes down the launch process with let you know via email.
5. The final step is to acknowledge that you know that the launch process will create AWS resources and click the "Create" button.

## Other Helpful Information

 - AWS SES requires that all emails be verified as working emails that can be accessed by you. So, the 1st time you use an email address a verification email is sent to the email and you must respond to it by clicking on a link.
 - Some email services block emails that come from AWS SES. For example, my work email blocks emails from AWS SES. So, if you don't receive an expected email from AWS SES this is probably the reason.
 - Also, my gmail account was putting emails from AWS SES in my spam folder. To keep this from happening, I setup my gmail account to allow any email I send to myself (The launcher sends emails to you but says the emails came from the same email you provide).
 - The launch process creates 4 AWS resources that aren't deleted when the stack is deleted: an EIP used by the Master and ECL Watch, a ssh keypair, an s3 bucket, and volumes that are attached to each instance of the cluster. These resources must be deleted manually AFTER the stack has been deleted (if you want them deleted). Also, each resource has the stack name in its Name which can be used to find them.
