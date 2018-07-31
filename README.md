The Docker Image contains the aws-cli and kubectl. It is used to update the AWS ECR credentials periodically in a kubernetes cluster.

# Setup

You need to add your credentials inside the file **aws-ecr-secrets.yml**.

You need to change the values of the environment variables in **ecr-cron.yml**.
- AWS_ACCOUNT
- AWS_REGION
- NAMESPACES (eg: default infrastructure)

Also you need to set your AWS_ACCOUNT, AWS_REGION and NAMESPACES in ecr-cron.yml.

Set up before:

	config-aws.sh

After you should be able to see the cron job with:

	kubectl get cronjobs -n infrastructure
