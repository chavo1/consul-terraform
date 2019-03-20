# This repo contains a demo of [Consul](https://www.consul.io/) cluster in AWS using [module](https://github.com/chavo1/consul-terraform)
## Prerequisites

- Please install the following component:

  - | [Terraform](https://www.terraform.io/)

You must also have an AWS account. You will need to set up your AWS credentials and needed variables in "example.tfvars" file. 

### We are now ready to go.
```
git clone https://github.com/chavo1/consul-terraform.git
cd consul consul-terraform 
```
- Create a terraform.tfvars file with following content:
```
access_key = "< Your AWS Access_key >"
secret_key = "< Your AWS Secret_key >"
key_name = ""
region = ""
instance_type = ""
subnet = "< VPC subnet ID >"
client_count = 2
server_count = 2
```

### We can start with deploying process
```
terraform init
terraform plan
terraform apply
```
### Do not forget to destroy the environment after the test
```
terraform destroy
```

### To test you will need Kitchen:

Kitchen is a RubyGem so please find how to install and setup Test Kitchen for developing infrastructure code, check out the [Getting Started Guide](http://kitchen.ci/docs/getting-started/).
For more information about tests please check the next link:

Than simply execute a following commands:

```
kitchen converge
kitchen verify
kitchen destroy
```
- The output from the test for 1 Consul server and 1 Consul client should as follow
```
Command: `terraform state list`
     ✔  stdout should include "module.consul-terraform.aws_instance.client[0]"
     ✔  stderr should include ""
     ✔  exit_status should eq 0
  Command: `terraform state list`
     ✔  stdout should include "module.consul-terraform.aws_instance.server[0]"
     ✔  stderr should include ""
     ✔  exit_status should eq 0
  Command: `terraform state list`
     ✔  stdout should include "module.consul-terraform.aws_instance.client[1]"
     ✔  stderr should include ""
     ✔  exit_status should eq 0
  Command: `terraform state list`
     ✔  stdout should include "module.consul-terraform.aws_instance.server[1]"
     ✔  stderr should include ""
     ✔  exit_status should eq 0
  http GET on http://ec2-54-82-99-129.compute-1.amazonaws.com:80
     ✔  status should cmp == 200
  http GET on http://ec2-54-82-99-129.compute-1.amazonaws.com:8500/ui/dc1/nodes
     ✔  status should cmp == 200
  http GET on http://ec2-54-82-99-129.compute-1.amazonaws.com:8500/ui/dc1/services/web
     ✔  status should cmp == 200
  http GET on http://ec2-34-227-207-153.compute-1.amazonaws.com:8500/ui/dc1/nodes
     ✔  status should cmp == 200
  http GET on http://ec2-34-227-207-153.compute-1.amazonaws.com:8500/ui/dc1/services/web
     ✔  status should cmp == 200
  http GET on http://ec2-54-83-64-254.compute-1.amazonaws.com:80
     ✔  status should cmp == 200
  http GET on http://ec2-54-83-64-254.compute-1.amazonaws.com:8500/ui/dc1/nodes
     ✔  status should cmp == 200
  http GET on http://ec2-54-83-64-254.compute-1.amazonaws.com:8500/ui/dc1/services/web
     ✔  status should cmp == 200
  http GET on http://ec2-54-196-135-51.compute-1.amazonaws.com:8500/ui/dc1/nodes
     ✔  status should cmp == 200
  http GET on http://ec2-54-196-135-51.compute-1.amazonaws.com:8500/ui/dc1/services/web
     ✔  status should cmp == 200

Test Summary: 22 successful, 0 failures, 0 skipped
```
