
pipeline {
    agent any
    parameters {
        string(name: 'image_tag', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    }
   
    stages {
        
        stage('Parameters') {
            steps {
                echo "Hello ${params.image_tag}"
                 
            }
        }
        
         stage('Logging into AWS ECR') {
            steps {
                script {
                sh "aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"
                }
                 
            }
        }
        
       
        
  
   
    }
}
