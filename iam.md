# IAM (Identity and Access Management)

AM gives you a large amount of functionality out of the box:

* Granular permissions
* Password rotation policy
* Identity federation (AD, Google, Facebook)
* MFA
* Set up temporary access
* Integrates with various AWS services
* PCI DSS compliant

Users = end users (people)
Groups = a collection of users under one set of permissions (e.g. finance, HR, sysadmins, superusers)
Roles = can be assigned to AWS resources (e.g. an EC2 instance can be assigned a role to enable access to S3)
Policies = a document that defines one or more permissions. Can be attaches to users, groups and roles
Permission = define access to AWS functionality in terms of actions (what can be done, e.g. create S3 bucket) and resources (what the actions can be applied to)

Policies can be attached directly to users - this is indicated in the console (if part of a group, this is shown with a link to the group).

Username and password are used to manually log into the AWS console.
Access Key ID and Secret Keys are used to programatically access AWS resources. Can never use password for this and vice versa.

For billing access, you need to both:
- Add the billing role
- Allow access to billing from non-root accounts

PowerUser = access to all AWS resources except IAM