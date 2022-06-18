##  Faisal Aduko Wahabu  | Deployed an high availability web app using CloudFormation.

In this project, I deployed web servers for a highly available web app using CloudFormation. The code creates and deploys the infrastructure and application for an Instagram-like app from the ground up. The steps involved deploying the networking components, followed by servers, security roles and software

This projects consist broadly of two parts:

1. Diagram: First developed a diagram that is a visual aid to understand the CloudFormation script.
2. Script (Template and Parameters): The second part is to reference from the diagram and create a matching CloudFormation script.

# Diagram of Architecture
![Web application](https://user-images.githubusercontent.com/39354209/174417013-52ca2f6e-27c4-4138-8133-d0585cbd7d0e.png)

#  Server specs
A Launch Configuration is created for the application servers in order to deploy four servers, two located in two different private subnets. The launch configuration will be used by an auto-scaling group.
Two vCPUs and at least 4GB of RAM is secured. The Operating System used is Ubuntu Linux Machine (Ubuntu 18.04). The instance type is t3.medium and the Machine Image (AMI) is ami-0ac73f33a1888c64a, with an allocated 10GB of disk space. 

#  Security Groups and Roles
Created an IAM Role named FaisalProject2_S3_Access that allows my instances the permission to use the S3 Service through Read Only Access rule.
Udagram communicates on the default HTTP Port: 80, as an inbound port opened to be used with the Load Balancer and the Load Balancer Health Check. Outbound traffic is unrestricted to nable the servers download and update their software.
The load balancer allows all public traffic (0.0.0.0/0) on port 80 for inbound and port 80 Outbound to reach the internal servers.
The application is deployed into the private subnets with a Load Balancer located in a public subnet.

# Output
The output exports of the CloudFormation script is a public URL of the LoadBalancer's DNS Name. 
The DNS Name URL is http://proje-webap-szwoa26ljxqt-616873406.us-west-2.elb.amazonaws.com/
![Echo Message From Website](https://user-images.githubusercontent.com/39354209/174416933-b6cdc483-10b3-4295-8f49-b341d3d3adf8.PNG)


# Dependencies
1. AWS account
You would require to have an AWS account to be able to build cloud infrastructure.

2. VS code editor
An editor would be helpful to visualize the image as well as code.

# How to run the supporting material?

You can run the supporting material in two easy steps:
1. Ensure that the AWS CLI is configured before runniing the command below
2. Create the network infrastructure
3. Check the region in the create.sh file
RUN Create: ./create.sh myFirstStack network.yml network-parameters.json
4. Create servers
5. Change the AMI ID and key-pair name in the servers.yml
6. Check the region in the update.sh file
RUN Update: ./update.sh mySecStack servers.yml server-parameters.json

