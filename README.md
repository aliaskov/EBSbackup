#Lambda EBS Backup

AWS Lambda based on py script will create backups, with frequency, according to backup tag.
After creating a backup tag "DeleteAfter" will be added and used later for purging old snaps. DeleteAfterDate - is a human readable date.
Number of snapshots can me set manually, by editing Retention tag. Default values are 30 snaps made once per day.

Add tag "Backup" to vol to start backup process.

ENV variables:

REGION = eu-west-1
DEFAULT_RETENTION = 30
AWS_ACCOUNT = AWS account num.
TZ = Europe/Berlin


Available backup tags for volumes:
Name: Backup
Value:
 ''
 'daily':
 '1/day':
 'true':
 '4/day':
 '6/day':
 '8/day':
 '12/day':
 '24/day':
 'hourly':

Name: Retention
Value: 1-9999
 Default retention is 30, could be set manually with tag "Retention" and value "XX"

 ![EBS Volume tagging example](/example-tagged-volume.png)

 Lambda config:
 - Runtime: Python 2.7
 - Handler: lambda_function.lambda_handler
 - Role: [role as specified below]
 - Memory: 128
 - Timeout: 5 sec
 - Add a trigger using "CloudWatch Events - Schedule", set for "rate(1 day)"

 IAM Lambda Role:
 ```
 {
     "Version": "2012-10-17",
     "Statement": [
         {
             "Effect": "Allow",
             "Action": [
                 "logs:*"
             ],
             "Resource": "arn:aws:logs:*:*:*"
         },
         {
             "Effect": "Allow",
             "Action": [
                 "ec2:DescribeVolumes",
                 "ec2:DescribeSnapshots",
                 "ec2:CreateSnapshot",
                 "ec2:DeleteSnapshot",
                 "ec2:CreateTags",
                 "ec2:ModifySnapshotAttribute",
                 "ec2:ResetSnapshotAttribute"
             ],
             "Resource": [
                 "*"
             ]
         }
     ]
 }
 ```


 ![EBS Volume output example](/output.png)
