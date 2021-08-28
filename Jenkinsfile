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
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp samplewebapp:latest'
                //sh 'docker tag samplewebapp samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry(credentialsId: '3d36c726-8563-479d-9af7-035ade8d1dc5', url: 'https://hub.docker.com/repository/docker/ashishut')  {
          sh  'docker push samplewebapp:latest'
        //sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 samplewebapp"
 
            }
        }
 
    }
	}
    
