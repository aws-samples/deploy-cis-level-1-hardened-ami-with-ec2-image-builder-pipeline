# Deploying CIS Level 1 hardened AMIs with Amazon EC2 Image Builder
The repository includes all the necessary files necessary to deploy a CIS Level 1 hardened image with Amazon EC2 Image Builder. Note that the tasks related with hardening the instance are outdated and therefore, the Amazon Inspector detects some security benchmarks as failing. Feel free to update the tasks or modifiy them to your liking.

## AWS Services Used

    AWS CloudFormation – AWS CloudFormation allows you to use domain-specific languages or simple text files to model and provision, in an automated and secure manner, all the resources needed for your applications across all Regions and accounts. You can deploy AWS resources in a safe, repeatable manner, and automate the provisioning of infrastructure.

    AWS KMS – Amazon Key Management Service (AWS KMS) is a fully managed service for creating and managing cryptographic keys. These keys are natively integrated with most AWS services. You use a KMS key in this post to encrypt resources.

    Amazon S3 – Amazon Simple Storage Service (Amazon S3) is an object storage service utilized for storing and encrypting data. We use Amazon S3 to store our configuration files.

    AWS Auto Scaling – AWS Auto Scaling allows you to build scaling plans that automate how groups of different resources respond to changes in demand. You can optimize availability, costs, or a balance of both. We use Auto Scaling to manage Nginx on Amazon EC2.

    Launch templates – Launch templates contain configurations such as AMI ID, instance type, and security group. Launch templates enable you to store launch parameters so that they don’t have to be specified every time instances are launched.

    Amazon Inspector – This automated security assessment service improves the security and compliance of applications deployed on AWS. Amazon Inspector automatically assesses applications for exposures, vulnerabilities, and deviations from best practices.

## Features
You deploy the following CloudFormation templates. These CloudFormation templates have a great deal of configurations. They deploy the following resources:

    vpc.yml – Contains all the core networking configuration. It deploys the VPC, two private subnets, two public subnets, and the route tables. The private subnets utilize a NAT gateway to communicate to the internet. The public subnets have full outbound access to the IGW.

    kms.yml – Contains the AWS KMS configuration that we use for encrypting resources. The KMS key policy is also configured in this template.

    s3-iam-config.yml – Contains the launch configuration and autoscaling groups for the initial Nginx launch. For updates and patching to Nginx, we use Image Builder to build those changes.

    infrastructure-ssm-params.yml – Contains the Systems Manager parameter store configuration. The parameters are populated by using outputs from other CloudFormation templates.

    nginx-config.yml – Contains the configuration for Nginx. Additionally, this template contains the network load balancer, target groups, security groups, and EC2 instance AWS Identity and Access Management (IAM) roles.

    nginx-image-builder.yml – Contains the configuration for the Image Builder pipeline that we use to build AMIs.

## How to use?
To deploy this project follow the step by step instructions found here.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

