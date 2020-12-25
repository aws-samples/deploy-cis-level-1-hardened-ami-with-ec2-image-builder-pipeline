# Deploying CIS Level 1 hardened AMIs with Amazon EC2 Image Builder
In this post, we demonstrate how to create an automated process that builds and deploys Center for Internet Security (CIS) Level 1 hardened AMIs. The pattern that we deploy includes Image Builder, a CIS Level 1 hardened AMI, an application running on EC2 instances, and Amazon Inspector for security analysis. You deploy the AMI configured with the Image Builder pipeline to an application stack. The application stack consists of EC2 instances running Nginx. Lastly, we show you how to re-hydrate your application stack with a new AMI utilizing AWS CloudFormation and Amazon EC2 launch templates. You use Amazon Inspector to scan the EC2 instances launched from the Image Builder-generated AMI against the CIS Level 1 Benchmark.

## Motivation
A common scenario AWS customers face is how to build processes that configure secure AWS resources that can be leveraged throughout the organization. You need to move fast in the cloud without compromising security best practices. Amazon Elastic Compute Cloud (Amazon EC2) allows you to deploy virtual machines in the AWS Cloud. EC2 AMIs provide the configuration utilized to launch an EC2 instance. You can use AMIs for several use cases, such as configuring applications, applying security policies, and configuring development environments. Developers and system administrators can deploy configuration AMIs to bring up EC2 resources that require little-to-no setup. Often times, multiple patterns are adopted for building and deploying AMIs. Because of this, you need the ability to create a centralized, automated pattern that can output secure, customizable AMIs.

After going through this exercise, you should understand how to build, manage, and deploy AMIs to an application stack. The infrastructure deployed with this pipeline includes a basic web application, but you can use this pattern to fit many needs. After running through this post, you should feel comfortable using this pattern to configure an AMI pipeline for your organization.

## Tech/framework used
Image Builder allows you to develop an automated workflow for creating AMIs to fit your organization’s needs. You can streamline the creation and distribution of secure images, automate your patching process, and define security and application configuration into custom AWS AMIs. In this post, you use the following AWS services to implement this solution:

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
