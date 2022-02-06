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
Create docker
Publish docker image on ECR
Create Task
Create Service with ALB and Autoscaling
Create pipeline deploying to ECS.

# Create cluster(ECS CLI)
cd  "C:\Program Files\Amazon\ECSCLI\"
ecs-cli configure --cluster ec2-ecs-lab --default-launch-type EC2 --config-name ec2-ecs-lab --region sa-east-1
ecs-cli configure profile --access-key xxxxxxxxxxxxxxx --secret-key xxxxxxxxxxxxx --profile-name ecs-cli-profile
ecs-cli up --capability-iam --size 2 --instance-type t2.micro --cluster-config ec2-ecs-lab --ecs-profile ecs-cli-profile

# Fargate
The same container can be run in the fargate server.
- Create a load Balancer
- Create a target group for port 8080 with path /
- Security group for ALB must allow outbound all traffic rules from ECS security group
- Security group for ALB must allow inbound rules for 8080 or ECS Security group.
- Create ECS Cluster
- Create service with load balancer and auto scaling
- Security group for ALB must allow outbound all traffic rules from ALB security group
- Security group for ECS allow inbound rules for 80 or ECS Security group.
- https://www.youtube.com/watch?v=cmRZleI18Yg

# Reference
https://dev.to/raphaelmansuy/deploy-a-docker-app-to-aws-using-ecs-3i1g
whizlab courses