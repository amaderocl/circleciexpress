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
					sh "docker ps -a | awk \'{ print \$1,\$2 }\' | grep circleciexpress | awk \'{print \$1 }\' | xargs -I {} docker rm -f {}"
					sh 'docker rmi -f circleciexpress'
				    sh "docker build -t circleciexpress ./"
					sh 'docker images'
            }
        }
        stage('Run') {
            steps {
			    
                echo 'Running'
				sh "docker run -d -p 8090:8080 circleciexpress"
				echo 'ir a la URL http://localhost:8090'
            }
        }
    }
}
