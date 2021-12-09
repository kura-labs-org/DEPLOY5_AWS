# Deployment 5: Building a VPC

### Objectives
**Let's use a VPC utilizing both a public and private subnet to securely access Jenkins**

### Step 1: Private EC2
We configured Jenkins on an EC2 launched in the private subnet. We then make a target group pointing to this EC2 and an Application Load Balancer that uses this target group.

*Note, the load balancer takes a while to set up. Give it a couple of minutes before moving on. The status will read `Active`*

### Step 2: Configuring Jenkins

Next access Jenkins using the url of the ALB. Setup the 2nd EC2 in the private subnet as the node. Jenkins will use this EC2 to build jobs.

**Two screenshots in this repo: `Agent Node Conn...` shows the node connecting, and the `Topology.png` shows a logical architecture of this system.**