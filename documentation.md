# Not Finished. I'm Gradually updating this documentation as I learn more about this project. 
# Deploymen 5 Documentation

## step 1. Create a Virtual Private Network (VPC) on AWS. Please visit https://docs.aws.amazon.com/directoryservice/latest/admin-guide/gsg_create_vpc.html to learn how.
## step 2. Create [0] Subnets within our VPC I'm Using [1] class C IP Addresses [2] RFC 1918 (reserved private internet addresses) Range (192.169.0.0 to 192.168.255.254) with a CIDR block of [3]/18 which allows us a total of 16,384 addresses for our network. Divide your Network into 4 subnets 2 private and 2 public. we will put distibute them across two [4]AZ's or Availavility zones 

## Please visit the Links below if you are unfamiliar with any of these terms:

### [0] Subnets : https://www.techtarget.com/searchnetworking/definition/subnet
### [1] Ip classes: https://www.computerhope.com/jargon/i/ip.htm
### [2] RFC 1918: https://netbeez.net/blog/rfc1918/
### [3] CIDR Blocks: https://networkproguide.com/wp-content/uploads/CIDR-IPv4-Subnet-Mask-Cheat-Sheet.png
### [4] Availablity zones: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html

## step 3. Add an Internet gateway to your VPC in order to able to use the internet from inside our VPC. visit this link to learn about internet gateways https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html
## step 4. Add a Network Address Translation gateway to your VPC, this help in resolving the addresses of the privates subnets in order for them to commuinicate with the internet through pulic subnets. Please visit this link to learn more about NAT gateways https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html 
## step 5. Create a routing table to associate the Internet gateway with the public subnets and the Nat gateway with the private subnets. Visit this link to learn more about Routing tables https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html
## step 6. Create an EC2 named JumpHost inside the VPC we just create and add it to the first public subnet, create a  security group with a rule that allows SSH access from Anywhere. 0.0.0.0/0 port: 22.
## step 7. Create an EC2 named Private inside the VPC we just create and add it to the first private subnet, create a security group with a rule that only allows SSH access from the security group assigned to the JumpHost EC2. port:22 sg-JumpHost and a rule that allows access to port 8080.  you will also have to install jenkins in your private EC2.
## step 6. Create an EC2 named Agent inside the VPC we just create and add it to the first private subnet, create a  security group with a rule that allows SSH access from Anywhere. 0.0.0.0/0 port: 22.
## step 8. Create a Target group and register your private EC2 and make sure it is listening to port 8080 on the private EC2.
## step 9. Create a load balancer within the VPC that we just created and add the security group of the public EC2 to allow it to access the private EC2 and fordward the private's 8080 port to its own 80 port and then we are able to access any application running on the private EC2 in this case jenkins.
## step 10. Use the load balance's endpoint to access your jenkins application running on the private EC2.
##
