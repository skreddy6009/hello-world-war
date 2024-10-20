//add 
pipeline { 
  agent { label 'slave' } 
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
     stage('docker container'){ 
    steps{ 
      script {
                    def userInput = input(
                        id: 'UserInput', message: 'Do you approve to proceed?', parameters: [
                            string(defaultValue: '', description: 'Enter your comments (optional):', name: 'Comments'),
                            choice(choices: ['Yes', 'No'], description: 'Proceed?', name: 'Proceed')
                        ]
                    )
                    
                    echo "User input received: ${userInput['Comments']}, Proceed: ${userInput['Proceed']}"   sh "docker stop saty3"
                    sh "docker rm saty3"
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
