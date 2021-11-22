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
                         sh '''#!/bin/bash
       
# Print Hello world message
echo "Hello World!"           
         '''                 
           sh "cd ./project/Manavae-web-app-2/Java-Ansible && mvn clean package"


                 }
            }   
        

        
        }
   }
