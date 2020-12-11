#### Create a new Launch Config
```
aws autoscaling create-launch-configuration --launch-configuration-name <unique_launch_config_name> --image-id <cis_level_1_ami_id> --instance-type <value> --iam-instance-profile <value> --security-groups <value> --associate-public-ip-address
```

#### Example
```
aws autoscaling create-launch-configuration --launch-configuration-name launch-config-2 --image-id ami-XXXXXX --instance-type <instance_type> --iam-instance-profile NginxBlueGreen-NginxInstanceProfile-XXXXXX --security-groups sg-XXXXXX --associate-public-ip-address
```

#### Get the Nginx Proxy Stack ID
```
aws cloudformation list-exports | grep <input_nginx_proxy_stack_name>
```

#### Example
```
aws cloudformation list-exports | grep NginxProxies
```

#### Get the Nginx Proxies Stack Outputs
```
aws cloudformation list-exports --query "Exports[?ExportingStackId=='<input_stack_name>']"
```

#### Example
```
aws cloudformation list-exports --query "Exports[?ExportingStackId=='arn:aws:cloudformation:us-east-1:<account_number>:stack/NginxProxies/XXXXXX-XXXXXX-XXXXXX -XXXXXX-XXXXXX']"
```

#### Update ASG with new Launch Config
```
aws autoscaling update-auto-scaling-group --auto-scaling-group-name <existing_asg_group_name> --launch-configuration-name <new_lc_name>
```

#### Example
```
aws autoscaling update-auto-scaling-group --auto-scaling-group-name NginxProxies-NginxInstanceASG1-XXXXXX --launch-configuration-name NginxProxies-NginxInstanceLC-XXXXXX
```

#### Update ASG with new Launch Config Instances
```
aws autoscaling start-instance-refresh --auto-scaling-group-name <value> --preferences '{"InstanceWarmup": 120, "MinHealthyPercentage": 50}'
```

#### Example
```
aws autoscaling start-instance-refresh --auto-scaling-group-name NginxProxies-NginxInstanceASG1-XXXXXX --preferences '{"InstanceWarmup": 120, "MinHealthyPercentage": 50}' --region us-east-1
```
