pipeline {
    agent any
	
	  tools
    {
       maven "Maven 3.0.5"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/anisha-thakkar2020/CI-CD-using-Docker.git'
             
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
                sh 'docker tag samplewebapp anishamthakkar/samplewebapp:latest'
                //sh 'docker tag samplewebapp anishamthakkar/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry(credentialsId: 'dockerHub', url: '') {
		
          sh  'docker push anishamthakkar/samplewebapp:latest'
        //  sh  'docker push anishamthakkar/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 anishamthakkar/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.26.208 run -d -p 8003:8080 anishamthakkar/samplewebapp"
 
            }
        }
    }
	}
    
