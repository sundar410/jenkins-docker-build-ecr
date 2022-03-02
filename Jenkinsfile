pipeline {
    agent any
    environment {
        REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
    }
   
    stages {
        
        stage('Echoing Output') {
            steps {
                script{ 
                sh "echo $AWS_ACCOUNT_ID | echo $AWS_DEFAULT_REGION | echo $IMAGE_REPO_NAME | echo $IMAGE_TAG | echo $REPOSITORY_URI"
                }
            }
        }
        
         stage('Logging into AWS ECR') {
            steps {
                script {
                sh "aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"
                }
             }  
          }
       
    // Building Docker images
        stage('Building image') {
          steps{
            script {
              dockerImage = docker.build "${IMAGE_REPO_NAME}:${IMAGE_TAG}"
            }
          }
        }

        // Uploading Docker images into AWS ECR
        stage('Pushing to ECR') {
         steps{  
             script {
                    sh "docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} ${REPOSITORY_URI}:$IMAGE_TAG"
                    sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${IMAGE_TAG}"
             }
            }
          }
    }
}
