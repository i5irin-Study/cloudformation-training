# CloudFormation Training

```
aws s3api create-bucket \
  --bucket "your-bucket-name" \
  --create-bucket-configuration "LocationConstraint=your-region"
```

```
aws s3 cp network.yml s3://your-bucket-name/
aws s3 cp security.yml s3://your-bucket-name/
aws s3 cp application.yml s3://your-bucket-name/

aws cloudformation validate-template --template-body file://root.yml
aws cloudformation deploy \
    --stack-name "your-stack-name" \
    --template-file root.yml \
    --capabilities CAPABILITY_NAMED_IAM \
    --parameter-overrides \
      TemplateNetwork="your-bucket-url/network.yml" \
      TemplateSecurity="your-bucket-url/security.yml" \
      TemplateApplication="your-bucket-url/application.yml" \
      SSHFromAddress="your-global-ip/32"
```
**Running on SSM**

```
zip -r ansible.zip ansible
aws s3 cp ansible.zip s3://your-bucket-name/
```

Run Ansible from the AWS SSM console.

**Running in local**

Replace `hosts: localhost` in `ansible/setup.yml` with `hosts: web`.

Execute the following commands.
```
ansible-playbook -i inventory/hosts.yml ansible/setup.yml
```
