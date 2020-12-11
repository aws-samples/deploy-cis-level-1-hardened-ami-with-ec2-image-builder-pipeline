#### USAGE:
```
This template creates Systems Manager Parameter Store values which are used for automating the installation of AWS Services.
```

#### EDIT: infrastructure-ssm-parameters.json
- NginxConfigStackName
- NetworkStackName


#### RUN: deploy infrastructure-ssm-parameters

```
aws cloudformation create-stack \
--stack-name <stack_name> \
--template-body file://<file_path>/infrastructure-ssm-params.yml \
--parameters file://<file_path>/infrastructure-ssm-parameters.json  \
--capabilities CAPABILITY_IAM \
-—region <us-east-1 or us-east-2>

```

**Example**
```
aws cloudformation create-stack --stack-name Infra-SSM-Params --template-body file://Templates/infrastructure-ssm-params.yml --parameters file://Parameters/infrastructure-ssm-parameters.json --capabilities CAPABILITY_IAM --region us-east-1
```
