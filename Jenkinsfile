pipeline {
environment {
        
        AWS_DEFAULT_REGION = "us-east-1"
    }
agent  any
stages {
                stage('checkout') {
            steps {
                 script{

                        
                            git "https://github.com/GarvitKushwaha/Terraform.git"			    
                        
                    }
                }
            }      
        
         stage('Maven - WAR creation') {
            
                 steps{
                         echo "Hello World"
                         sh '''rm -rf ./project
mkdir project
git -C ./project clone https://github.com/GarvitKushwaha/Maven-web-app.git
'''
                         sh "cd ./project/Maven-web-app/Java-Ansible && mvn clean package"
       


                 }
            }  
         stage('jFrog artifactory'){
        steps{
                sh "cd ./project/Maven-web-app/Java-Ansible && mvn deploy"
        }
        }
        stage('Terraform Plan') {
            steps {
                     withCredentials([vaultString(credentialsId: 'AWS_ACCESS_KEY_VAULT', variable: 'AWS_ACCESS_KEY'), vaultString(credentialsId: 'AWS_SECRET_KEY_VAULT', variable: 'AWS_SECRET_KEY')]) {
                bat 'cd&cd terraform/Terraform & terraform init -input=false'
                bat 'cd&cd terraform/Terraform & terraform destroy -auto-approve'
                bat "cd&cd terraform/Terraform & terraform plan -input=false -out tfplan"
                bat 'cd&cd terraform/Terraform & terraform show -no-color tfplan > tfplan.txt'
                     }
            }
        }
       

        stage('Terraform Apply') {
            steps {
                    withCredentials([vaultString(credentialsId: 'AWS_ACCESS_KEY_VAULT', variable: 'AWS_ACCESS_KEY'), vaultString(credentialsId: 'AWS_SECRET_KEY_VAULT', variable: 'AWS_SECRET_KEY')]) {
                bat "cd&cd terraform/Terraform & terraform apply -input=false tfplan"
                    }
            }
        
        }
        
        }
   }
