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
              
                sh 'docker build -t samplewebapp2:latest .' 
                sh 'docker tag samplewebapp2 sona09/myrepo:samplewebapp2'
                //sh 'docker tag samplewebapp samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry(toolName: 'Docker', url: 'https://hub.docker.com/repository/docker/sona09/myrepo') {
          //sh  'docker push sona09/samplewebapp:latest'
		sh 'docker push sona09/myrepo:samplewebapp2'
        //sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 sona09/myrepo:samplewebapp2"
 
            }
        }
 
    }
	}
    
