# fail2ban for AWS ELB

You can use this solution, if you have AWS EC2 webservers and you want use fail2ban for attack block.
This action adds and removes deny role to AWS VPC Network ACL if jail is triggered. With this solution, the banned ip cant connect to the ELB any more.

# How to use fail2ban for AWS ELB?

1. Copy aws-vpc-acl.conf to the fail2ban action.d directory, and modify the file for your configuration. (Read the comments in conf file)
2. Set the jail's action parameter: aws-vpc-acl
3. Config the apache2 like this: https://aws.amazon.com/premiumsupport/knowledge-center/log-client-ip-load-balancer-apache/
4. Create programmatic access user in AWS IAM with "AmazonVPCFullAccess" permission.
5. Configure this user for aws cli on ELB targeted instances.
6. Set the "role number" to 2000 in "permit any" role on your network ACL. (All the custom and default role's "role number" have to be over 2000)
7. Restart the fail2ban service on the servers.
