**AWS Account**: Container for all **resources**, with a global, isolated IAM (DB) for all **identities**.

May be good practice to create multiple AWS Accounts for different uses (prod, dev, test).


### IAM

 **Manages identities, authenticates and authorizes.**
#### Identities

All identities start with no permissions.

**Types:** 
- Users:
	- Unique ID For a Person or service
- Groups:
    - Users can belong to any number of groups.
- Policies:
	- A document of resource permissions(.json):
	- Can be assigned to: Users, Groups and roles.
	- Example:
```
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowWithMFAOnly",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::my-bucket",
      "Condition": {       # Optionaly
        "Bool": {
          "aws:MultiFactorAuthPresent": "true"
```
- Role:
    - Can be used by **AWS Services**, or for granting **external access** to your account (Like for ec2 instance)



**MFA is enabled per user, enforced per policy 'condition'**

#### IAM Access Keys

- Up to two keys per user for Long-term
- Used for CLI and SDK
- Keys are provided only at creation
- Example:
**Access Key ID:** ABABABABABABABA
**Secret Access Key:** oierWRhoefWORIOF/DFLWAnljef


