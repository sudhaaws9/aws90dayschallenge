AWS Lambda Function to Start and Stop an EC2 Instance


open lambda in aws console
create function one for stop Instance
##stopec2instance

    import boto3
    region = 'us-west-2'
    instances = ['i-09b308df6c7925549']
    ec2 = boto3.client('ec2', region_name=region)
    def lambda_handler(event, context):
        ec2.stop_instances(InstanceIds=instances)
        print('stopped your instances: ' + str(instances))

create policy for ec2 start and stop, and attach to iam role

    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "logs:CreateLogGroup",
                    "logs:CreateLogStream",
                    "logs:PutLogEvents"
                ],
                "Resource": "arn:aws:logs:*:*:*"
            },
            {
                "Effect": "Allow",
                "Action": [
                    "ec2:Start*",
                    "ec2:Stop*"
                ],
                "Resource": "*"
            }
        ]
    }

EC2 resource-level permissions provide a powerful means of controlling access to your EC2 resources.

create a lambda function for starting the stopped instance and attach to the role
##startec2instance

    import boto3
    region = 'us-west-2'
    instances = ['i-09b308df6c7925549']
    ec2 = boto3.client('ec2', region_name=region)
    def lambda_handler(event, context):
        ec2.start_instances(InstanceIds=instances)
        print('stopped your instances: ' + str(instances))


#If you want your users to be able to call DecodeAuthorizationMessage themselves, you’ll need to make sure the group has the following policy attached:

    {
    "Version": "2012-10-17",
    "Statement": [
        {
        "Effect": "Allow",
        "Action": ["sts:DecodeAuthorizationMessage"],
        "Resource": ["*"]
        }
    ]
    }

after that open cloudwatch in aws console
add a rule in event section of cloudwatch page
create rule
eventsource:Build or customize an Event Pattern or set a Schedule to invoke Targets.

In the eventsource section we have 2 options
1.event Pattern
2.Schedule
I choosen schedule
again we have 2 options 1. fixed rate of time 2.cron expression
I used fixed rate of 5 mintues

Target:elect Target to invoke when an event matches your Event Pattern or when schedule is triggered.
coming to target section of rules i added 2 targets

i used lambda functions stopec2instance and startec2instance in target section.
after that i configured yhe detailes

then i given the name to this rule as ec2stopandstart.