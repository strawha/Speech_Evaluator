pipeline{
    agent {
	docker {
	     image 'akshaymg99/speech-spe:latest'
	     args '-v $HOME:/SPE_Speech_Evaluator'
	  }
    }
    
    stages{

        stage('SCM git pull'){
            steps{
                git credentialsId: 'github', 
                url: 'https://github.com/akshaymg99/SPE_Speech_Evaluator.git'
            }
        } 

	stage('Docker Build'){
            steps{
                sh "docker build . -t akshaymg99/speech-spe:latest "
            }
        }
	
	stage('Testing') {
	    steps{
                sh 'cd /SPE_Speech_Evaluator'
		sh 'ls -l'
		sh 'pwd'
		sh 'python3 manage.py test'		
	    }
	}

	stage('DockerHub Push'){
            steps{
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
                    sh "docker login -u akshaymg99 -p ${dockerHubPwd}"
                }
                sh "docker push akshaymg99/speech-spe:latest "
            }
            
        }   

            
    }
  
}
