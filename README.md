[![Docker Pulls](https://img.shields.io/docker/pulls/frekele/aws-ecr-kubectl.svg)](https://hub.docker.com/r/frekele/aws-ecr-kubectl/)
[![Docker Stars](https://img.shields.io/docker/stars/frekele/aws-ecr-kubectl.svg)](https://hub.docker.com/r/frekele/aws-ecr-kubectl/)
[![GitHub issues](https://img.shields.io/github/issues/frekele/aws-ecr-kubectl.svg)](https://github.com/frekele/aws-ecr-kubectl/issues)
[![GitHub forks](https://img.shields.io/github/forks/frekele/aws-ecr-kubectl.svg)](https://github.com/frekele/aws-ecr-kubectl/network)
[![GitHub stars](https://img.shields.io/github/stars/frekele/aws-ecr-kubectl.svg)](https://github.com/frekele/aws-ecr-kubectl/stargazers)

The Docker Image contains the aws-cli and kubectl.

It is used to update the AWS ECR credentials periodically in a kubernetes cluster.

# Setup

You need to add your credentials inside the file **aws-ecr-secrets.yml**.
- aws-access-key-id: YOUR-AWS-ACCESS-KEY-ID
- aws-secret-access-key: YOUR-AWS-SECRET-ACCESS-KEY

Secrets need to be converted to base64. Eg:

	echo -n 'AMJZ7XOS5QSYJKIAJ5Q4' | base64


You need to change the values of the environment variables in **ecr-cron.yml**.
- AWS_ACCOUNT: YOUR-AWS-ACCOUNT
- AWS_REGION: YOUR-AWS-REGION
- NAMESPACES YOUR-K8S-NAMESPACES (eg: infrastructure default test dev)

Set up:

	./config-aws.sh

After you should be able to see the cron job with:

	kubectl get cronjobs -n infrastructure

AWS IAM Policy:

	{
	    "Version": "2012-10-17",
	    "Statement": [
		{
		    "Effect": "Allow",
		    "Action": [
			"ecr:GetAuthorizationToken",
			"ecr:BatchCheckLayerAvailability",
			"ecr:GetDownloadUrlForLayer",
			"ecr:GetRepositoryPolicy",
			"ecr:DescribeRepositories",
			"ecr:ListImages",
			"ecr:DescribeImages",
			"ecr:BatchGetImage"
		    ],
		    "Resource": [
			"*"
		    ]
		}
	    ]
	}

Built-based on the blog post:
 - https://medium.com/@damitj07/how-to-configure-and-use-aws-ecr-with-kubernetes-rancher2-0-6144c626d42c
