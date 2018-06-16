# fail2ban for AWS ELB

With this solution you can protect your EC2 web servers hosted on AWS behind an Application Load Balancer using fail2ban. This custom action adds and removes deny rules to the VPC ACL instead of the hosts iptables. In this way the IP addresses of the attackers are getting blocked by AWS and malicious traffic generated by them can't reach your instances, not even your Application Load Balancer.

# How to use fail2ban for AWS ELB?

1. Copy aws-vpc-acl.conf to the fail2ban action.d directory, and modify the file for your configuration. (Read the comments in conf file)
2. Set the jail's action parameter: aws-vpc-acl
3. Config the apache2 like this: https://aws.amazon.com/premiumsupport/knowledge-center/log-client-ip-load-balancer-apache/
4. Set AWS IAM role with "AmazonVPCFullAccess" permission for aws cli on ELB targeted instances.
5. Set the "rule number" to 2000 in "permit any" role on your network ACL. (All the custom and default role's "rule number" have to be over 2000)
6. Restart the fail2ban service on the servers.
