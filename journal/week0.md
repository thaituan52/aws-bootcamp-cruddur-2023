# Week 0 — Billing and Architecture

## Setup Instructions:
_ [Create a new User and Generate AWS Credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorials.html):

In IAM of AWS, create a new user with admin access control and get their access key for later use (down CSV file or paste in somewhere).


_ [Install AWS CLI using Linux:](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)  

```sh
cd workspace
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

then

```sh
aws sts get-caller-identity
```
At this point, we are unable to locate credentials (Haven't set the environment variables at this point yet). We can:

_ Configure credentials by running:
```sh
aws configure
```

_ [Setup environment variables](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html) using the credentials we have:

```sh
export AWS_ACCESS_KEY_ID="AWS_ACCESS_KEY_ID"
export AWS_SECRET_ACCESS_KEY="AWS_SECRET_ACCESS_KEY"
export AWS_DEFAULT_REGION= "AWS_DEFAULT_REGION"
```
*Change export -> gp env to make it permanent*

Result after:  
```json
{
    "UserId": "user_id",
    "Account": "account_id",
    "Arn": "arn:aws:iam::account_id:user/thaituando"
}
```

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
*Due to the reason that this project try to use only free tier service of AWS, this service will not be needed too much but for future use, this one is put into project for the project owner learn more about how to setup billing and budget here. Additionally, all of this creations can be done via AWS website manually*
_Budgets: 

This work use [cost and usage budget](https://docs.aws.amazon.com/cli/latest/reference/budgets/create-budget):

```sh
aws budgets create-budget \
    --account-id $AWS_ACCOUNT_ID \
    --budget file://aws/json/budget.json \
    --notifications-with-subscribers file://aws/json/budget-notifications-with-subscribers.json 
```

_SNS for Billing alert: 
To [create an SNS topic](https://docs.aws.amazon.com/cli/latest/reference/sns/create-topic): 

```sh
aws sns create-topic \
    --name my-topic
```
-> TopicArn -> [A subscription supply the TopicARN and our Email](https://docs.aws.amazon.com/cli/latest/reference/sns/subcription)

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


## Reference & Notes:
_Setup token: 
```sh
git remote set-url origin https://$TOKEN@github.com//thaituan52/aws-bootcamp-cruddur-2023.git 
```

_[Reference for AWS CLI](https://docs.aws.amazon.com/cli/latest/reference/)

_All of the keys in this file are replaced with names/words for secuirty reasons






