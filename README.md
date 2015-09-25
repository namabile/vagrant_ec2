```
# configure aws; us-east-1 as default location
$ aws configure

# create security group
$ aws ec2 create-security-group --group-name devenv-sg --description "security group for development environment in EC2"

# allow incoming traffic on port 22
$ aws ec2 authorize-security-group-ingress --group-name devenv-sg --protocol tcp --port 22 --cidr 0.0.0.0/0

# create key-pair
$ aws ec2 create-key-pair --key-name devenv-key --query 'KeyMaterial' --output text > devenv-key.pem
```
