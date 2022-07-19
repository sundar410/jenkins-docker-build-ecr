def awsCredentials = [[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws_account']]

pipeline {
    agent any
    parameters {
        string(name: 'kpiimagetag', defaultValue: 'Mr Jenkins', description: 'Please mention image tag version')
    }
   
    stages {
        
        stage('Parameters') {
            steps {
                echo "Hello ${params.kpiimagetag}"
                 
            }
        }
        
         stage('Logging into AWS ECR') {
            steps {
                script {
                 withCredentials(prodawsCredentials){
                        sh "aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"
                 }
                }   
            }
        }
        
       
        
  
   
    }
}
