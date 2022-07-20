def awsCredentials = [[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws_account']]

pipeline {
    agent any
    parameters {
//         choice(choices: 'kpi\nlogging\nresource\nspecimen\nmetric', name: 'servicename', description: 'Please mention the service name Below')
        string(name: 'versionid', description: 'Please mention the version id value Below')
        
    }
   
    stages {
        
        stage('Parameters') {
            steps {
                script {
                   if ("${params.versionid}" == ""){ 
                     echo "Hello ${params.versionid} Empty value"
               }
                  else { 
                     echo "Hello ${params.versionid} !!!!!!!!"
                 }  
                }
              
                 
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
                   
                          sh "docker pull ${REPOSITORY_URI}/${IMAGE_REPO_NAME}:${params.servicename}-${params.versionid}"
                      
                      }
                    }
                  }  
               }
         
        
        stage('Rollbacking to the previous version') {
            steps {
                script {
                 withCredentials(awsCredentials){
                        sh "docker tag  ${REPOSITORY_URI}/${IMAGE_REPO_NAME}:${params.servicename}-${params.versionid} ${REPOSITORY_URI}/${IMAGE_REPO_NAME}:${params.servicename}"
                        sh "docker push ${REPOSITORY_URI}/${IMAGE_REPO_NAME}:${params.servicename}"
                        
                 }
                }   
            }
        }
        
       
        
  
   
    }
}
