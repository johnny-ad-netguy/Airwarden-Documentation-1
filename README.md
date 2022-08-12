# Airwarden Documentation

Airwarden server will be deployed using the EC2 t3.xlarge class instances.  We use a certificate chain for the *airwarden.tech domain for HTTPs.  

# Configuring AWS ALB for Airwarden

Create the ALB, assign the subnets it will load-balance for.  Each subnet being load-balanced must have a route to the IGW.  Choose the configured certificate from ACM & a security policy.

# Security Groups

Security groups need to be configured for the ALB and the EC2's.  For the ALB, allow http and https from any; for the EC2's, allow tcp/9000 from the ALB security group.  Additionally, add rules for the engineering team to access directly while staging the deployment. 


# The apache service that runs on the server uses port 443, airwarden is running on nodejs, on TCP port 9000.  To accomplish getting the URL configured correctly:

1.  Create a target group for the customer EC2's, select the targets by instances
2.  On the ALB, setup 2 listeners, 1 for HTTP and 1 for HTTPs
3.  For the HTTP listener, configure a rule to redirect to HTTPs 
4.  For the HTTPs listnener, insert a rule for fouting by hostname to the target group
5.  In DNS, create CNAME record to point the hostname to the ALB




