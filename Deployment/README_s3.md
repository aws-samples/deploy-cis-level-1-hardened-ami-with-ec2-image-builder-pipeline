#### USAGE:
```
Generic KMS Encrypted S3 bucket with built in Security Controls that restrict both public access to the Bucket as well any unencrypted connections to the Bucket.
```

#### EDIT: s3-params.json
- TeamName
- BucketName
- KMSMasterKeyAlias
- RoleName

#### RUN: deploy s3

```
aws cloudformation create-stack \
--stack-name <stack_name> \
--template-body file://<file_path>/s3-bucket.yaml \
--parameters file://<file_path>/s3-params.json \
--capabilities CAPABILITY_IAM -—region <us-east-1 or us-east-2>
```

**Example**
```
aws cloudformation create-stack --stack-name <stack_name>-S3 --template-body file://Templates/s3-bucket.yaml --parameters file://Parameters/s3-params.json --capabilities CAPABILITY_IAM --region us-east-1
```
