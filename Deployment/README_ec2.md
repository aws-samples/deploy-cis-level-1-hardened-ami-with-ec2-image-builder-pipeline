#### USAGE:
```
Provisions an EC2 Instance, a Security Group, and Systems Manager Session Manager Permissions. This CloudFormation Template deploys an Instance Profile to enable Session Manager to connect to the instance.

The purpose of using Session Manager is to allow users to connect to EC2 Instances without have to traverse the internet. Additionally, using Session Manager allows users to not have to open any ports to connect to their instances. 
```

#### EDIT: vpc-params.json
- InstanceType
- NetworkStackName
- SGGroupName
- EnvironmentName
- EC2InstanceName
- SessionManagerRoleName
- SessionManagerPolicyName

#### RUN: deploy vpc

```
aws cloudformation create-stack --stack-name <stack_name> --template-body file://<file_path>/ec2-instance-template.yml --parameters file://<file_path>vpc-private-params.json  --capabilities CAPABILITY_IAM -—region <us-east-1 or us-east-2>
```

**Example**
```
aws cloudformation create-stack --stack-name EC2-Test --template-body file://Templates/ec2-instance-template.yml --parameters file://Parameters/ec2-params.json --capabilities CAPABILITY_NAMED_IAM --region us-east-1

```
