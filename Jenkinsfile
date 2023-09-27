pipeline {
    agent any
    environment {
                AWS_ACCESS_KEY_ID = credentials('aws-creds')
                AWS_SECRET_ACCESS_KEY = credentials('aws-creds')
            }

    stages { 
        stage ('Terraform Init - provision EKS infrastructure') {
            steps {  
                echo 'initializing terraform' 
                script {

                        sh "terraform init"
                }
            }  
        }
        stage ('Provision eks- Terraform plan') {
            steps {  
                echo 'terraform plan' 
                script {  
                        sh "terraform plan"
                }
            }  
        }
        stage ('Provision eks- Terraform apply') {
            steps {  
                echo 'applying terraform code' 
                script {
                     
                        sh "terraform apply -auto-approve"
                    
                }
            }  
        }
        stage ('Update kube-config') {
            steps {  
                echo 'updating kubeconfig' 
                script {
                       
                        sh "aws eks update-kubeconfig --name pet-clinic"
                    
                }
            }  
        }
    }
}
