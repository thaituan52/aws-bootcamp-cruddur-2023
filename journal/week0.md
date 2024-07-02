# Week 0 — Billing and Architecture

## Setup Instructions:
_ [Create a new User and Generate AWS Credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorials.html):

In IAM of AWS, create a new user with admin access control and get their access key for later use (down CSV file or paste in somewhere).


_ [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) using Linux: 

```sh
cd workspace
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

->

```sh
aws sts get-caller-identity
```
Unable to locate credentials. You can configure credentials by running "aws configure".
(Haven't set the environment variables at this point yet)

_ [Setup environment variables](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html) using the credentials we have:

```sh
export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_DEFAULT_REGION= ""
```

replace '' with your access keys
change export -> gp env to make it permanent

*We can lose all of the AWS CLI setup so we gonna make the gitpod environment to get this setup everytime we get into it by updating gitpod.yml (a file to prepare and build a project in Gitpod)*
```yml
tasks:
  - name: aws-cli
    env:
      AWS_CLI_AUTO_PROMPT: on-partial
    init: |
      cd /workspace
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install
      cd $THEIA_WORKSPACE_ROOT
```

## AWS Budget and SNS
_Budgets: 
*Due to the reason that this project try to use only free tier service of AWS, I will not need it too much but for future use, this one is put into project for me to learn more about how to setup billing and budget here.*

I am working on cost and usage budget (deprived from */budgets/create-budget*):

```sh
aws budgets create-budget \
    --account-id $AWS_ACCOUNT_ID \
    --budget file://aws/json/budget.json \
    --notifications-with-subscribers file://aws/json/budget-notifications-with-subscribers.json 
```

_SNS for Billing alert: 
To create an SNS topic (deprived from */sns/create-topic*): 
```sh
aws sns create-topic \
    --name my-topic
```
-> TopicArn -> a subscription supply the TopicARN and our Email - sns/subcription

```sh
aws sns subscribe \
    --topic-arn TopicARN \
    --protocol email \
    --notification-endpoint your@email.com
```

- [Create an Alarm via AWS CLI](https://repost.aws/knowledge-center/cloudwatch-estimatedcharges-alarm)
- We need to update the configuration json script with the TopicARN we generated earlier
- We are just a json file because --metrics is is required for expressions and so its easier to us a JSON file.

```sh
aws cloudwatch put-metric-alarm --cli-input-json file://aws/json/alarm_config.json
```


## Reference:
[Setup token](git remote set-url origin https://$TOKEN@github.com//thaituan52/aws-bootcamp-cruddur-2023.git )

[Reference for AWS CLI](https://docs.aws.amazon.com/cli/latest/reference/)

[Json files]( file://aws/json/)





