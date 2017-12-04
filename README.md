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
