# Week 0 — Billing and Architecture
Setup Instructions:
_Install AWS CLI in https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html using Linux: 
cd workspace
<!-- curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install -->

->aws sts get-caller-identity
Unable to locate credentials. You can configure credentials by running "aws configure".
(Haven't set the environment variables at this point yet)

_Setup environment variables using https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html -> credentials
<!-- export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_DEFAULT_REGION= "" -->
replace it with your access keys

*We can lose all of the AWS CLI setup so we gonna make the gitpod environment to get this setup everytime we get into it by updating gitpod.yml
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



