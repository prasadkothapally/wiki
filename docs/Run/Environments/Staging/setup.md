# Setup

Infrastructure in staging environment is provisioned using OpenTofu scripts

## OpenTofu

Installing tooling

```
sudo apt-get update

sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
```
Set up the OpenTofu repository

Firstly, we need to make sure that we have a copy of the OpenTofu GPG key. This verifies that our packages have indeed been created using the official pipeline and have not been tampered with.

```
sudo install -m 0755 -d /etc/apt/keyrings

curl -fsSL https://get.opentofu.org/opentofu.gpg | sudo tee /etc/apt/keyrings/opentofu.gpg >/dev/null

curl -fsSL https://packages.opentofu.org/opentofu/tofu/gpgkey | sudo gpg --no-tty --batch --dearmor -o /etc/apt/keyrings/opentofu-repo.gpg >/dev/null

sudo chmod a+r /etc/apt/keyrings/opentofu.gpg /etc/apt/keyrings/opentofu-repo.gpg
```

Now create the OpenTofu source list

```
echo \
  "deb [signed-by=/etc/apt/keyrings/opentofu.gpg,/etc/apt/keyrings/opentofu-repo.gpg] https://packages.opentofu.org/opentofu/tofu/any/ any main
deb-src [signed-by=/etc/apt/keyrings/opentofu.gpg,/etc/apt/keyrings/opentofu-repo.gpg] https://packages.opentofu.org/opentofu/tofu/any/ any main" | \  sudo tee /etc/apt/sources.list.d/opentofu.list > /dev/null
  
sudo chmod a+r /etc/apt/sources.list.d/opentofu.list
```

Installing OpenTofu
```
sudo apt-get update

sudo apt-get install -y tofu
```

## Infrastructure Provisioning using OpenTofu

We have a repository called "iac-aws-tofu" to store the tofu scripts.

Prerequisites:

- Make sure to install the OpenTofu before running the scripts.

Below are the instructions to run the infra provisioning scripts

```
tofu workspace select <workspace-name>   ( workspace refers to an environment, which might be dev/staging/prod )

tofu plan

tofu apply --auto-approve
```

## Infrastructure Setup by OpenTofu

Below are the AWS services setup by Opentofu after running the scripts


 Script          |         Service                              |   Configuration    
 ----------------|----------------------------------------------|------------------------
 VPC             |  VPC                                         |   10.0.0.0/16
                 |  2 Public Subnets                            |   10.0.1.0/24
                 |                                              |   10.0.2.0/24
                 |  2 Private Subnets                           |   10.0.3.0/24
                 |                                              |   10.0.4.0/24
                 |  Internet GateWay                            |  
                 |  NAT GateWay                                 |
                 |  Public Route Table                          |
                 |  Private Route Table                         |
 eks_cluster     |  Elastic Kubernetes Service                  |   Version 1.28
                 |  Launch template for Node Group              |
                 |  Nodegroup (EC2)                             |   Instance family - t3a.medium
                 |  EBS Volumes for nodes                       |   Volume type     - gp2
                 |  Cluster Autoscaler                          |
                 |  Application load balancer controller        |
 Bation          |  Bastion server to operate the EKS           |   Instance family - t2.micro
                 |  Elastic IP for Bastion Server               |
                 |  Default EBS volume                          |   Volume type     - gp2                                  
 PtInstance      |  Performance testing Server                  |   Instance family - m5a.xlarge      
                 |  Elastic IP for the same server              |
 BuildInstance   |  Build Server                                |   Instance family - t3a.large
                 |  Elastic IP for the same server              |
                 |  Default EBS Volume                          |   Volime type     - gp2
 DBInstance      |  Server to setup Databases, Message Broker   |   Instance family - m5a.large
                 |  EBS Volume                                  |   Volume type     - gp3
 rds             |  Postgres Database                           |   Version         - 14.11
                 |                                              |   Instance Class  - db.t4g.micro








