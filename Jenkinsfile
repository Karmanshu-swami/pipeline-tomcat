pipeline {
    
    agent {
        label "new_slave_pipeline"
    }
    
    
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/sr98877/pipeline-code.git'
            }
            
        }
        
        stage('Build by Maven Package') {
            steps {
                sh 'mvn clean package'
            }
            
        }
        stage('Deploy on testing') {
            steps {
		// sh 'pwd'
		sh "sudo docker build -t dockerimage:${BUILD_TAG} ."
		}
	}        
        stage('Pushing image to docker hub') {
            steps {
	        withCredentials([string(credentialsId: 'Docker_hub_passwd', variable: 'Docker_hub_passwd_var')]) {

		sh "sudo docker login -u srronak11 -p ${Docker_hub_passwd_var}"
		}
		sh "sudo docker push srronak/java-test-app:${BUILD_TAG}"

	}        
   
   }
    
    
}
