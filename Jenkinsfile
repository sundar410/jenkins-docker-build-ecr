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
                 withCredentials(awsCredentials){
                        sh "aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"
                 }
                }   
            }
        }
        
        stage('Pull the Docker images') {
              steps {
                  script {
                      withCredentials(awsCredentials){
                   
                          sh "docker pull ${REPOSITORY_URI}/${IMAGE_REPO_NAME}:${params.kpiimagetag}"
                      
                      }
                    }
                  }  
               }
         
        
        stage('Rollbacking to the previous version') {
            steps {
                script {
                 withCredentials(awsCredentials){
                        sh "docker tag  ${REPOSITORY_URI}/${IMAGE_REPO_NAME} ${REPOSITORY_URI}/${IMAGE_REPO_NAME}:kpi"
                        sh "docker push ${REPOSITORY_URI}/${IMAGE_REPO_NAME}:kpi"
                        
                 }
                }   
            }
        }
        
       
        
  
   
    }
}
