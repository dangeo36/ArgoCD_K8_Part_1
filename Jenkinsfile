pipeline {
    agent any
    environment {
                AWS_ACCESS_KEY_ID = credentials('aws-creds')
                AWS_SECRET_ACCESS_KEY = credentials('aws-creds')
            }
    parameters {
        choice(name: 'action', choices: ['apply', 'destroy'], description: 'Terraform action')
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
        stage ('Terraform Action') {
            steps {  
                echo 'Terraform action is -->${action}' 
                script {

                        sh "terraform ${action} -auto-approve"
                    
                }
            }  
        }
        stage ('Update kube-config') {
            when {
                expression { params.action != 'destroy' }
            }
            steps {  
                echo 'updating kubeconfig' 
                script {
                       
                        sh "aws eks update-kubeconfig --region us-east-1 --name pet-clinic"
                    
                }
            }  
        }
    }
}
