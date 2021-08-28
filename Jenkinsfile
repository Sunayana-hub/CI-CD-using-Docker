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
                sh 'docker tag samplewebapp sona09/samplewebapp:latest'
                //sh 'docker tag samplewebapp samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry(credentialsId: 'eeea852e-a8d8-4666-afc6-711598f84132', url: 'https://hub.docker.com/repository/docker/sona09/myrepo') {
          sh  'docker push sona09/samplewebapp:latest'
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
    
