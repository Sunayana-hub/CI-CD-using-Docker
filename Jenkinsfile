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
              
                sh 'docker build -t samplewebapp1:latest .' 
                sh 'docker tag samplewebapp1 sona09/myrepo:samplewebapp1'
                //sh 'docker tag samplewebapp samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: ""]) {
          //sh  'docker push sona09/samplewebapp:latest'
		sh 'docker push sona09/myrepo:samplewebapp1'
        //sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 sona09/myrepo:samplewebapp1"
 
            }
        }
 
    }
	}
    
