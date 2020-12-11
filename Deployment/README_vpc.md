#### USAGE:
```
This template creates a Multi-AZ (two Availability Zones), multi-subnet VPC infrastructure and associates one Non RFC 1918 CIDR Block to the newly created VPC.

This template also deploys VPC endpoints which allow communication to AWS Services without having to traverse the internet.
```

#### EDIT: vpc-params.json
```
- VPCCIDR
- Environment
- AvailabilityZones
- PublicSubnet1ACIDR
- PublicSubnet2ACIDR
- PrivateSubnet2Z1CIDR
- PrivateSubnet2Z2CIDR
- PrivateSubnet4Z1CIDR
- PrivateSubnet4Z2CIDR
```

#### RUN: deploy vpc
```
aws cloudformation create-stack \
--stack-name <stack_name> \
--template-body file://<file_path>/vpc.yml \
--parameters file://<file_path>vpc-params.json  \
--capabilities CAPABILITY_IAM \
-—region <us-east-1 or us-east-2>
```

**Example**
```
aws cloudformation create-stack --stack-name VPC-Sandbox00 --template-body file://Templates/vpc.yml --parameters file://Parameters/vpc-params.json --capabilities CAPABILITY_IAM --region us-east-1
```
