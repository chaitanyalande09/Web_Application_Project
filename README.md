# Deployment of Hotstar clone application using Jenkins CI/CD
This repo depicts the deployment of sample Hotstar clone application built using JavaScript code. DevOps, an amalgamation of Development and Operations, emphasizes the integration and automation throughout the software development lifecycle. The deployment process encompasses the utilization of various tools and services.

In real world scenario Organisation keep the source code on central repository for versioning and follows a specific branching strategy according to their need (like gitflow, trunkbased etc). For demonstration purpose I have used only one branch named master and have kept source code and other files in the same branch. We will use the master branch for deployment of our code.

## Tools and Technologies:-
* AWS Cloud Provider for tech stack hosting
*	Ubuntu 22.04 
*	Git and Github for SCM
*	Jenkins for CI/CD
*	Docker for containerization of application
*	Terraform for infrastructure provisioning
*	Ansible for configuration management
*	AWS EKS for kubernetes stack
*	Node.js-16 for javascript runtime environment
*	SonarQube for code quality analysis
*	Java-17 

## Setup:-
The journey begins with the setup of an AWS EC2 instance configured with Ubuntu22.04, granting it a specific IAM role to facilitate the necessary access permission. Subsequently, an automated script is crafted to install terraform to provision cloud infrastructure using terraform.

* Provision the Ansible server, Jenkins master server and AWS EKS cluster using terraform scripts.
* Login to Ansible server and configure ssh authentication connection login for installing packages to Jenkins master server using Ansible playbook.
* Install packages such as Jenkins, Docker, AWS CLI, JAVA-17, kubectl.
* SSh login into Jenkins server and configure Jenkins, install necessary plugins such as Eclipse Temurin installer, Sonarqube Scanner, NodeJs, Docker, Docker-pipeline.
  - Install Global tools in Jenkins such as sonarqube latest version.
  - Run sonar qube container with latest version on Jenkins machine
  - Configure Sonar server and create quality gates. Create Web-Hook token for quality gates report result.
  - Add Dockerhub credentials into Jenkins to fetch and push docker image
  - Create declarative pipeline having following stages:-
    1. Fetch the code from repository
    2. SonarQube analysis
    3. Quality Gate result
    4. Install dependencies
    5. Docker Build and Push 
    6. Run the container with latest image
    7. Deploy to AWS EKS

* Before deploying the application to EKS using pipeline first run the cluster locally, then add the configuration of cluster stored in .kube/config file as secret file into Jenkins credentials.
* Ensure load balancer Ip address is added to cluster ec2 instance security group and copy load balancer end point, open it in browser to access web page.
