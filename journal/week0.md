# Week 0 — Billing and Architecture
Setup Instructions:
_Create a new User and Generate AWS Credentials:
in IAM of AWS, create a new user with admin access control and get their access key for later use (down CSV file or paste in somewhere).


_Install AWS CLI in https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html using Linux: 
cd workspace
<!-- curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install -->

->aws sts get-caller-identity
Unable to locate credentials. You can configure credentials by running "aws configure".
(Haven't set the environment variables at this point yet)

_Setup environment variables using https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html using the credentials we have:
<!-- export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_DEFAULT_REGION= "" -->
replace it with your access keys
change export -> gp env to make it permanent

*We can lose all of the AWS CLI setup so we gonna make the gitpod environment to get this setup everytime we get into it by updating gitpod.yml (a file to prepare and build a project in Gitpod)
<!-- tasks:
  - name: aws-cli
    env:
      AWS_CLI_AUTO_PROMPT: on-partial
    init: |
      cd /workspace
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install
      cd $THEIA_WORKSPACE_ROOT -->


*AWS Budget and SNS
_Budgets: 
*Due to the reason that this project try to use only free tier service of AWS, I will not need it too much but for future use, this one is put into project for me to learn more about how to setup billing and budget here.

*I am working on cost and usage budget:
<!-- aws budgets create-budget \
    --account-id $AWS_ACCOUNT_ID \
    --budget file://aws/json/budget.json \
    --notifications-with-subscribers file://aws/json/budget-notifications-with-subscribers.json  -->

The 2 json files are deprived from /budgets/create-budget

_SNS for Billing alert: - sns/create-topic
To create an SNS topic: 
aws sns create-topic \
    --name my-topic




*Reference:
command for setup token
<!-- git remote set-url origin https://<your_token>@github.com//thaituan52/aws-bootcamp-cruddur-2023.git 
-->


Reference for AWS CLI : https://docs.aws.amazon.com/cli/latest/reference/





