### Get the ARN of the Image Builder Role
```
aws iam list-roles --query "Roles[?RoleName == 'example-role'].[RoleName, Arn]"
```

### Assume the Image Builder role using the ARN provided from previous step
```
aws sts assume-role --role-arn "arn:aws:iam::123456789012:role/example-role" --role-session-name AWSCLI-Session
```

### Using the Content from the previous step update the following environment variables
```
export AWS_ACCESS_KEY_ID=RoleAccessKeyID
export AWS_SECRET_ACCESS_KEY=RoleSecretKey
export AWS_SESSION_TOKEN=RoleSessionToken
```

### Double check that you have assumed the correct role
```
aws sts get-caller-identity
```

### Create a prefix in existing S3 bucket called components only if it is not already there
```
aws s3api put-object --bucket demobucket23232142 --key components/
```


### Create zip nginx proxy file for linux-cis directory
```
zip -r linux-cis.zip LinuxCis
```

### Upload linux cis zip file to a S3 bucket
```
aws s3 cp linux-cis.zip s3://demobucket23232142/components/
```


### Create zip Nginx config file for Nginx directory
```
zip -r nginx.zip Nginx
```

### Upload Nginx zip file to a S3 bucket
```
aws s3 cp nginx.zip s3://demobucket23232142/components/
```

### Upload ansible cis playbook file to a S3 bucket
```
aws s3 cp AnsibleConfig/cis_playbook.yml s3://demobucket23232142/components/
```

### Upload ansible nginx playbook file to a S3 bucket
```
aws s3 cp AnsibleConfig/nginx_playbook.yml s3://demobucket23232142/components/
```


### Upload ec2 Imagebuilder Component file
```
aws s3 cp AnsibleConfig/component-nginx.yml s3://demobucket23232142/components/
```

aws cloudformation create-stack \
--stack-name ib-nginx00 \
--template-body file://Templates/nginx-image-builder.yml \
--parameters file://Parameters/nginx-image-builder-params.json \
--capabilities CAPABILITY_NAMED_IAM \
--region us-east-1
