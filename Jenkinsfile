
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
        sh "docker build -t application:v3 ." 
      }
    }
  } 
     stage('docker container'){ 
    steps{ 
      script{ 
        sh "docker run-itd --name saty3 -p 9000:8080 application:v3 " 
      }
    }
  }  
  } 
}
