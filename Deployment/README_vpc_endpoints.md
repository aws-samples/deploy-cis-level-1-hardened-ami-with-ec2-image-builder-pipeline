#### USAGE:
```
This template also deploys VPC endpoints which allow communication to AWS Services without having to traverse the internet.
```

#### RUN: deploy vpc endpoints

```
aws cloudformation create-stack \
--stack-name <stack_name> \
--template-body file://<file_path>/vpc-endpoints.yml \
--parameters file://<file_path>/vpc-endpoint-params.json  \
--capabilities CAPABILITY_IAM \
--region <us-east-1 or us-east-2>

```

**Example**
```
aws cloudformation create-stack \
--stack-name VPC-Dev-Endpoint00 \
--template-body file://Templates/vpc-endpoints.yml \
--parameters file://Parameters/vpc-endpoint-params.json \
--capabilities CAPABILITY_IAM \
--region us-east-1
```