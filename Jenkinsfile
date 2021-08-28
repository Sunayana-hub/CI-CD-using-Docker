pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
	
	stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/Sunayana-hub/CI-CD-using-Docker.git'
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp4:latest .' 
                sh 'docker tag samplewebapp4 sona09/myrepo:samplewebapp4'
                //sh 'docker tag samplewebapp samplewebapp:$BUILD_NUMBER'
               
          }
        }
     stage('Login') {
      steps {
        sh './login.sh'
      }
    }
  stage('Publish image to Docker Hub') {
          
            steps {
	sh 'docker push sona09/myrepo:samplewebapp4'
        //sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
                          
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 sona09/myrepo:samplewebapp4"
 
            }
        }
 
    }
	}
    
