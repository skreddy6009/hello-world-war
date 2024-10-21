//add 
pipeline { 
  agent { label 'slavenode1' } 
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
        sh "docker build -t application:${BUILD_NUMBER} ." 
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
               docker stop saty3 || true 
               
               docker rm saty3 || true

                sh "docker run -itd --name saty3 -p 9000:8080 application:${BUILD_NUMBER}"    
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
