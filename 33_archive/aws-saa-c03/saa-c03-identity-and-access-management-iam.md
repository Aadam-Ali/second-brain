---
id: 20221121205221
tags: [aws-saa-c03, iam]
---

# Identity and Access Management (IAM) (SAA-C03)

## Securing the Root Account

* Enable MFA on the root account
* Create and admin group for administrators and assign relevant
  permissions
* Create user accounts for administrators and them to the administrator
  group

## IAM Policy Documents

* Allows permissions to be written as JSON
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```

## Key Points

* IAM is global
* The Root Account - this is the account created when setting up an AWS
  account and it has full admin access. It should not be used for day to
  day tasks
* New Users - when created, a new user has no permissions
* Access Keys - these allows programmatic access to AWS, CLI / SDK. They
  can only be retrieved once.
* Password Policies - should be setup
* IAM Federation - Use existing user accounts / credentials (e.g. AD) by
  setting up Federation
* Identity Federation - Uses the SAML standard, essentialy, AD
