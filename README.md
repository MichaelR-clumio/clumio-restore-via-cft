clumio-restore-via-cft give an example of an AWS CloudFormation template that creates the infrastrucutre to to support EC2 instances in a new account/region and then runs Clumio restore commands to deploy those EC2 instances from backups taken in Clumio
The CFT allows the user to select via parmaeters the criteria to use when selecting which backups to restore.  This criteria in this example includes:
  - AWS Source Region
  - AWS Source Account ID
  - AWS resource tags

The Clumio restore is run via Clumio APIs launched via a custom lambda function (part of the CFT).  This lambda function requires a lambda layer (python package) to be pulled in when the CFT runs.  The CFT is setup to pull in this lambday layer from a S3 bucket.  The requirement is that the bucket needs to be in the same region where the CFT is being deployed AND the user running the CFT needs permissions to that bucket.  To accomplish this the CFT has two paramters to define this S3 locaiton.  Note:  The lambda layer would need to be copied into this locaiton prior to running the CFT.

When lauchned (if successfull), there are no actions required upon the part of the user to setup the environment and to recover the EC2 instances.  This would all happen as part of the CFT.  If there are errors, you might have to look at the cloud watch logs for the custom lambda function to see what went wrong.
