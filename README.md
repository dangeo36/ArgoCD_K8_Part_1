# ArgoCD_K8
The goal of this project is to automate Kubernetes manifest files with ArgoCD and Jenkins. The CI portion of the pipeline will build Docker images of a Java application and push them to Amazon ECR. Images are pushed with a build number (or tag) that can be referenced later in the CD portion. The CD portion will pull the latest tag and update the Kube manifest files. Once everything is properly updated, ArgoCD will monitor the latest changes in the pipeline and update accordingly. 

# Part 1
For this part of the project, we will be using Terraform to provision our Amazon EKS cluster and node groups. We will also be building out a custom VPC and assigning the right policies so that we can use EBS. This process will be automated with Jenkins. Our Jenkinsfile will also include Build Parameters that can correspond to 'terraform apply' or 'terraform destroy' depending on the desired outcome. 

Part 2 GitHub Repo: https://github.com/dangeo36/ArgoCD_K8_Part_2.git 

# Tools / Dependencies
For this project, I have an Amazon EC2 instance (Ubuntu 20.04, t2.medium) that has Java 17, Jenkins, Terraform, awcli (configured with proper credentials), kubectl, and Docker. 


