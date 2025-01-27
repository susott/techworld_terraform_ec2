# Create AWS EC2 instance with Terraform

With this code, you can set up an AWS EC2 instance with terraform, along with related aws infrastructure, such as VPN, subnet,
security group, internet gateway and route table.

On the created EC2 instance of type t2.micro it will install the latest amazon linux image. Ports 22 (ssh) and 8080 (tcp) are open for incoming traffic. However, ssh access is only allowed from certain ips, which can be configured trough the my_ip (cidr block) variable.

Finally, a shell script (see entry_script.sh) will run on the created instance, which will install and run docker and nginx.

The code is part of the Terraform module of the [Techworld with Nana DevOps Bootcamp](https://www.techworld-with-nana.com/devops-bootcamp).

# Set up

To use the terraform code, you need to have an aws account with read and write access for the respective resources. The credentials can e.g. be stored in an .aws/credentials file in your home directory. More information can be found in the [aws documentation about configuration and credential file settings](https://docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html)

Furthermore it's recommended to create your own terraform.tfvars file within this repo. It needs to define the following six variables. Alternatively, enter the variables when executing terraform commands.

```
vpc_cidr_block = "TODO"
subnet_cidr_block = "TODO"
avail_zone = "eu-central-1b"
env_prefix = "TODO, could be eg. 'dev' or 'prod'"
my_ip = "TODO"
public_key_location = "TODO location of your own (local) public key"
```

# Usage

* Make sure that you have terraform installed
* Run `terraform plan` to see if anything is missing or what resources would be created
* Run `terraform apply`to actually create resource. Afterwards, you should be able to ssh into the server and see an nginx start page on port 8080. The public IP address will be shown in the output section from the apply command on your terminal.
* Run `terraform destroy` to clean up all the resources that got created.
