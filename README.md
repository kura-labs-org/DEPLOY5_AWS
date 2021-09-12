# DEPLOY5_AWS
<h1 align=center>Deployment 5</h1>

Welcome to deployment 5, for this deployment you will need to follow the directions in the deployment5.pdf. Once you have build your secure Jenkins network, you will need to create a network topology of your redundant and secure Jenkins architecture.     

- Be sure to include the following below in your pull request: 

***Requirements:*** 
- [x]Create your network topology and submit the file to this repository.
- [x]Include security group rules you made, to your topology. Also include where you attached each policy.
- [x]Take a screenshot of you logged into your Jenkins master and the agent connecting to the Jenkins master(also include the Url in the screenshot).
- [x]One screenshot is required, so you have the option of choosing how you would like to submit it. 

👉Link to deployment instructions: [here](https://github.com/kura-labs-org/DEPLOY6_AWS/blob/main/Deployment%235.pdf)  


<h1>Documentation</h1>
  Changed AZ to Oregon us-west-2
VPC Create:
Name: Production-ENV-test
IPv4 CIDR: 192.168.1.0/24

Subnet:
public1 us-west-2a
192.168.1.0/26
public2 us-west-2b
192.168.1.64/26
public1 us-west-2a
192.168.1.128/26
private 
192.168.1.192/26


Internet Gateway:
Created internet gateway
Attach the gateway to Production-ENV-test(VPC)

Route Table:
public us-west-2a
192.168.1.0/25 via local
0.0.0.0/0 via IG

private route: 192.168.1.128/24	local
set explicit association to subnet(private)


Security Groups:
Name: Any Access
Details: Provides all outbound and single SSH inbound.
VPC: Production-ENV-test(VPC)
Inbound: myip:22 . my-ip:8080
Outbound: 0.0.0.0:0

Name: Any Access
Details: Provides all outbound and single SSH inbound.
VPC: Production-ENV-test(VPC)
Inbound: Any Access(SG):22
Outbound: 0.0.0.0:0


Instances:
master
default settings on everything
change VPC to Production-ENV-test(VPC)
change subnet to public
change security group to Any Access

bootstrap:
```
#!/bin/bash
sudo amazon-linux-extras install java-openjdk11
sudo amazon-linux-extras install epel
sudo wget -O /etc/yum.repos.d/jenkins.repo \
https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum upgrade
sudo yum install epel-release java-11-openjdk-devel
sudo yum install jenkins
sudo systemctl start jenkins
```
Set up jenkins.
Set up the target group
Set up load balancer
Went to master and set up agent.
Agent had issues due to lack of java.
Created Nat Gateway targeting public1 and added an elastic IP
Attached route to subnet

Following this, install java on the agent.
Agent 1 will be online in Jenkins Node

~~Privatize the networks.
Clone the AMI for jenkins main.
Create EC2 Jump Drive with SG Any Access and same key in public1
Redeploy image of mainJ in private1 subnet
Created Another Security Group to 8080 and 22 from public security group from jump EC2.





Cloned the Image
Redeployed on private subnet
