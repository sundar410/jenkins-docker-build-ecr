def awsCredentials = [[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws_account']]


pipeline {
    agent any
    environment {
        properties([[$class: 'ParametersDefinitionProperty', parameterDefinitions: [[$class: 'StringParameterDefinition', name: 'image_tags', defaultValue: 'notihing']]]])
//         REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
        echo "received ${binding.hasVariable('myparam') ? myparam : 'undefined'}"

    }
   
    stages {
        
//          stage('Logging into AWS ECR') {
//             steps {
//                 script {
//                 sh "aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"
//                 }
                 
//             }
//         }
//         stage('Build the Docker Image') {
//               steps {
//                   script {
//                   sh "docker pull -t ${IMAGE_REPO_NAME}:${IMAGE_TAG} ."
//                   }
//               }
//         }
//         stage('Push the Docker Image to the ECR') {
//               steps {
//                   script {
//                   sh "docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} ${REPOSITORY_URI}:${IMAGE_TAG}"
//                   sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${IMAGE_TAG}"
//                   }
//               }
//         }
//         stage('Deploy in the ECS') {
//               steps {
//                   script {
//                   sh "aws ecs update-service --cluster sundar-ecs-cluster --service nodeapp-svc  --force-new-deployment --region ${AWS_DEFAULT_REGION}"
//                   }
//               }
//         }
        
  
   
    }
}
