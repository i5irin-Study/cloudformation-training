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
    --parameter-overrides \
      TemplateNetwork="your-bucket-url/network.yml" \
      TemplateSecurity="your-bucket-url/security.yml" \
      TemplateApplication="your-bucket-url/application.yml"
```

```
ansible-playbook -i ansible/inventory/hosts.yml ansible/setup.yml
```
