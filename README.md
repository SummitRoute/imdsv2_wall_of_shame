# IMDSv2 Wall of Shame
The following vendors do not allow customers to enforce IMDSv2 in their accounts. More information about what this is, what AWS can do, and what you can do, can be found beneath this list.

- AWS Data Pipelines
- Databricks
- Juniper vSRX
- [Okta ASA agent](https://help.okta.com/asa/en-us/Content/Topics/Adv_Server_Access/docs/aws-overview.htm)
- [Palo Alto Networks Prisma Cloud](https://prismacloud.ideas.aha.io/ideas/PANW-I-3889)
- SAS Viya
- Tecton

## How accurate is this list?
Where possible, I've linked to public support pages or Github issues for the vendors that confirm the vendor does not support IMDSv2. If that does not exist, then I have relied on multiple reports from customers (in all cases at least one such customer is someone I know personally). I have also reached out to the vendors to let them know they are on this list so they can provide corrections if this is not true. Check the commit history of this repo to see when this list was last updated.


---------------------------------
# What is IMDSv2?
In the wake of the [2019 Capital One breach](https://krebsonsecurity.com/2019/07/capital-one-data-theft-impacts-106m-people/), AWS [released](https://aws.amazon.com/blogs/security/defense-in-depth-open-firewalls-reverse-proxies-ssrf-vulnerabilities-ec2-instance-metadata-service/) IMDSv2 as a way of mitigating SSRF attacks against EC2s that could steal the credentials of their IAM roles.
By default, EC2s still allow the old Instance MetaData Service (IMDSv1) and so special action must be taken to require IMDSv2.  The insecurity of IMDSv1 has been presented at major security conferences for years, such as [Black Hat](https://www.youtube.com/watch?v=2NF4LjjwoZw) in 2014.


## Enforcing IMDSv2
Real-world guidance on how to make the needed updates to support IMDSv2 can be found [here](https://docs.google.com/document/d/1X737xoQviufdxZk_l33bnpp6noOmNIYvMilQCdhtwoY/edit).

Enforcing IMDSv2 can be done using the SCP found [here](https://summitroute.com/blog/2020/03/25/aws_scp_best_practices/#require-the-use-of-imdsv2). This has to be applied with caution though because a number of applications and unfortunately vendors may still require IMDSv1.

# Goal of this project
I want to improve the security of all customers on AWS by better enabling them to apply the security best practice of enforcing IMDSv2. This includes eradicating IMDSv1 from vendors and making IMDSv2 enforcement the default on AWS.

## How will this goal be accomplished?
I am going to list the vendors here that are not allowing their customers to follow security best practices by not allowing them to enforce IMDSv2.
I will be reaching out to these vendors to ensure they are aware of this project and request they provide timelines on their improvement.
I have a number of requests to AWS themselves to improve the ability to enforce IMDSv2, and this includes making it a requirement of vendors to enforce IMDSv2. As such, any vendors that are harmful to the security of AWS customers should be delisted from the AWS Partner network.

# Requests to AWS
The recent [BreakingFormation](https://orca.security/resources/blog/aws-cloudformation-vulnerability/) security incident had questionable impact, but it did show that AWS's own production EC2s, that internally run the CloudFormation service, are not enforcing IMDSv2.  As a result of AWS not implementing their own advised security best practices, they fell victim to an attack that IMDSv2 was specifically created to defeat.  AWS controls the entire platform and ecosystem, and security is publicly described as "job zero" at AWS: Therefore, they should be the most capable of implementing security best practices on themselves, but it was shown they have not. Security incidents of cloud providers themselves [are becoming more common](https://github.com/SummitRoute/csp_security_mistakes) and they have an obligation to customers to implement security best practices.

I have requested that AWS do the following to make it easier for both themselves and their customers to enforce IMDSv2. 

1. Add an ability to set a default account setting to enforce IMDSv2 much like they did for S3 Public Block Access. Creating an EC2 in the web console by default creates one that allows IMDSv1 and will result in an AccessDenied if you enforce IMDSv2 via an SCP.
2. Make it possible to see in the web console which EC2s do not enforce IMDSv2 and to enforce it.
3. Add a warning on the EC2 web console for any EC2s that allow IMDSv1, much like the IAM console warnings for no MFA on root.
4. Auto-decode EC2 Access Denied errors when the user has the sts:DecodeAuthorizationMessage privilege. Decoding these errors manually is a bad user experience. IMDSv2 enforcement via SCPs are currently a painful user experience because of this.
5. Require AWS Partners, Marketplace vendors, and anyone else you have influence over to use IMDSv2 for their products and solutions they deploy in customer environments.
6. Any AWS service or feature should support IMDSv2 enforcement. For example, the recent [EC2 fast launch](https://aws.amazon.com/about-aws/whats-new/2022/01/aws-speed-optimizations-windows-instances-ec2/) feature only supports IMDSv2 when used from the API, and not from the web console.

## Requests to you as a customer
- Please reach out to your AWS account teams to have them plus one my requests to AWS on your behalf.
- If you use any of the vendors listed, please request they update their products to support IMDSv2 enforcement.
- If you know of any other vendors that should be listed, please file issues or PRs against this repo.


## Requests to vendors
Ensure all your products allow IMDSv2 enforcement.

