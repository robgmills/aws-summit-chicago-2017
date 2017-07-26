# [Securing Your Cloud Investment: Mastering AWS Identity Access Management (IAM)](https://awschicago17.smarteventscloud.com/connect/sessionDetail.ww?SESSION_ID=128461)

## Abstract
The landscape of IT and data security has changed vastly since the advent of the cloud. Savvy technology leaders know that they must have visibility and control over their environment to fully leverage their cloud investments. Tools like IAM offer teams indispensable tools to proactively manage and protect their cloud environment. Join CloudCheckr CEO Aaron Newman to learn tips for effective and secure cloud deployments that you can implement today, including:

How to address requirements of the AWS Shared Responsibility Model
Why anticipating internal and external threats are crucial for mitigating security risks in the cloud
IAM overview and how it helps ensure secure and compliant deployments
Features and policies, as well as how to apply them to users and groups
Advice for leveraging IAM roles to mitigate potential security risks
Best practices for using IAM to configure user permissions, and other important considerations

## Notes

### IAM Best Practices
* reduce attack surface, eliminate risk
* humans are the weak link
* poor use of IAM is biggest security weakness

### Worst security vulnerability

### Real world example
* DoD data discovered on AWS server that was left unproctected
* Accessible s3 bucket
* Data not encrypted in the bucket
* S3 by default not public (_is this true?_)

### More examples
* Wrote a tutorial how to Amazon S3 wrong
* [http://flaws.cloud](http://flaws.cloud)
* `Any Authenticated AWS Users` means _anyone with an AWS account can get access_ not just those users in your account
* Shopify
* Bitcoin mining

### CIS Amazon Web Services Foundations
* Good guide/standards for IAM
* Read it and enforce it.

### Best Practices
#### 1. Use Federated Access from Outside AWS
* Don't use IAM
* Probably already have one that the security team is already looking at
* https://aws.amazon.com/iam/details/manage-federation

#### 2. Use IAM roles not accounts [sic: users] or access keys
* IAM access keys are just waiting to be leaked
    * Access keys accidentally checked into source control repositories
    * AWS scans Github/Gitlab/etc for access keys and disables
* Examples: cross-account roles, instance roles, etc.
* When using cross-account roles, don't forget about the [_confused depty problem_](https://wikipedia.org/wiki/Confused_deputy_problem).

#### 3. Rotate IAM access and secret access keys on a regular basis
* Don't forget rule #2 (don't use IAM access keys)
* At some point, developers see the keys.  What happens when the developer leaves the org?
* Set a policy for how often
* policy can vary based on situation (practicality, economics)
* wait to see how hard it is to actually accomplish
* https://aws.amazon.com/blogs/security/how-to-rotate-access-keys-for-iam-users/

#### 4. Don't leak your AWS access keys
* pushing to source control
* [what to do if you inadvertently expose an ews access key](https://aws.amazon.com/blogs/security/what-to-do-if-you-inadvertently-expose-an-aws-access-key/)

#### 5. Delete stale or unused access keys
* If an IAM access key is not being used, delete it
* More complicated deleting root access keys
* Create and publish a policy around aging of stale or unused 
* Look at aws method generate-credential-report

#### 6. Set your IAM Password Policies
* Account by account setting
* 9 paswsord policy options available
* [Official AWS documentation](http://docs.aws.amazon.com/IAM/latest/userGuide/id_credentials_passwords_account-policy.html)

#### 7. Don't grant permissions to IAM users, grant to IAM groups and assign users to groups
* Nothing new
* Managing user permissions is complex
* Control permissions to groups
* Assign users to groups
* Don't use _star_ (\*) i.e. `EC2:*`

#### 8. Find unused IAM accounts
* User left organization?
* Is a default password still on the account? _autogenerate individual new account passwords_
* Set originational policy on how long is unused or stale.

#### 9. Find accounts with permissions they don't actually need
* Principle of least privileges
* _Use IAM Access Advisor tab_

#### 10. Monitor All IAM Activity
* AWS CloudTrail reconds each time the AWS API is called
    * Currently supports most AWS services
    * You have to enable it in every account/regin
* Conveniently everything in AWS goes thrhough the API
    * Even actions in the AWS management console go through the API
* CloudTrail writes files into an Amazon S3 bucket
    * Near real-time (every 5 minutes)
    * Files are in JSON format

### Monitoring Reporting & optimization
CloudCheckr
* set global policies/practices and enforce them
* transparency of current settings
* 450 best practice checks - beyond security into utilization, resource allocation, etc




















