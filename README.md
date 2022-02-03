# AWS_ECS
Web Page deployed on ECS containers

# Install ECS on Windows
PS C:\> New-Item -Path 'C:\Program Files\Amazon\ECSCLI' -ItemType Directory
PS C:\> Invoke-WebRequest -OutFile 'C:\Program Files\Amazon\ECSCLI\ecs-cli.exe' https://amazon-ecs-cli.s3.amazonaws.com/ecs-cli-windows-amd64-latest.exe

# Install ECS on Linux
sudo curl -Lo /usr/local/bin/ecs-cli https://amazon-ecs-cli.s3.amazonaws.com/ecs-cli-linux-amd64-latest

# Build Docker Image
docker run -p 80:8080 -d node-web-app
curl http://localhost:80
docker build -t node-web-app .

# Objectives
Package and build a node application and package a simple node application with Docker
Create an ECR repository to store our Docker Image
Upload the Docker image to the repository
Create and launch an Elastic Container Cluster (ECR)
Launch our application as a task within the Elastic Container Cluster
Expose and open this application on the internet

# Create cluster(ECS CLI)
cd  "C:\Program Files\Amazon\ECSCLI\"
ecs-cli configure --cluster ec2-ecs-lab --default-launch-type EC2 --config-name ec2-ecs-lab --region sa-east-1
ecs-cli configure profile --access-key xxxxxxxxxxxxxxx --secret-key xxxxxxxxxxxxx --profile-name ecs-cli-profile
ecs-cli up --capability-iam --size 2 --instance-type t2.micro --cluster-config ec2-ecs-lab --ecs-profile ecs-cli-profile

# Reference
https://dev.to/raphaelmansuy/deploy-a-docker-app-to-aws-using-ecs-3i1g
whizlab courses