The Docker Image contains the aws-cli and kubectl. It is used to update the AWS ECR credentials periodically in a kubernetes cluster.

# Setup

You need to add your credentials inside the file **aws-ecr-secrets.yml**.
- aws-access-key-id: YOUR-AWS-ACCESS-KEY-ID
- aws-secret-access-key: YOUR-AWS-SECRET-ACCESS-KEY

You need to change the values of the environment variables in **ecr-cron.yml**.
- AWS_ACCOUNT: YOUR-AWS-ACCOUNT
- AWS_REGION: YOUR-AWS-REGION
- NAMESPACES YOUR-K8S-NAMESPACES (eg: default infrastructure)

Set up before:

	config-aws.sh

After you should be able to see the cron job with:

	kubectl get cronjobs -n infrastructure
