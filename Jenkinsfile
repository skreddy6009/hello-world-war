//add 
pipeline { 
  agent { label 'slave1' } 
  stages{ 
  stage('generte package'){ 
    steps{ 
      script{ 
        sh "mvn install" 
      }
    }
  } 
     stage('docker build'){ 
    steps{ 
      script{ 
        sh "docker build -t sudhakar24/devops/application:${BUILD_NUMBER} ." 
      }
    }
  } 
    stage('docker image pushing'){ 
    steps{ 
      script{ 
        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin" 
                        sh "docker push sudhakar24/devops/application:${BUILD_NUMBER}"
       }
      }
    }
  } 
stage('Deploy') {
            input {
                message 'Do you want to deploy to production?'
                ok 'Deploy!'
                parameters {
                    string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: 'Deployment environment')
                }
            }
             steps { 
             script{ 
                echo "Deploy"  
               //sh "docker stop saty3"
              // sh "docker rm saty3"
                sh "docker run -itd --name satya3 -p 9000:8080 sudhakar24/devops/application:${BUILD_NUMBER}" 
                
        } 
      } 
    }  
}
post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()  // This cleans the workspace at the end of the pipeline
        }
    }
}
