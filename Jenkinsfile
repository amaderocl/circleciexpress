pipeline {
   agent any
    stages {
        stage('test') {
		    agent {
                docker { image 'node:current-alpine3.12' }
             }
            steps {
               sh 'npm install'
			   sh 'npm start &'
			   sh 'npm test'
            }
        }
        stage('build') {
            steps {
                    echo 'Building.. Docker image'
		            sh 'docker -v'
					try {
                            sh 'docker rmi -f circleciexpress'
                        } 
						catch (Exception e) 
						{
                             sh 'no existe la imagen'
                        }
				    sh 'docker build -t circleciexpress ./'
					sh 'docker images'
            }
        }
        stage('Run') {
            steps {
			    
                echo 'Running'
				sh 'docker run -d -p 8090:8080 circleciexpress'
				echo 'ir a la URL http://localhost:8090'
            }
        }
    }
}
