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
        
        stage('Push the Docker Image to the ECR') {
              steps {
                  script {
                      withCredentials(awsCredentials){
                          sh "docker build -t ${IMAGE_REPO_NAME}:${params.kpiimagetag} ."
                          sh "docker tag ${IMAGE_REPO_NAME}:${params.kpiimagetag} ${REPOSITORY_URI}:${params.kpiimagetag}"
                          sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${params.kpiimagetag}"
                      }
                    }
                  }  
               }
         
        
//         stage('Logging into AWS ECR') {
//             steps {
//                 script {
//                  withCredentials(awsCredentials){
//                         sh "docker pull ${IMAGE_REPO_NAME}:${IMAGE_TAG}"
//                  }
//                 }   
//             }
//         }
        
       
        
  
   
    }
}
