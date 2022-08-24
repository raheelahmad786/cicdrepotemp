pipeline {
    environment {
        registry = "raheelahmad20/cicd" 
        registryCredential = 'dockerhub' 
       // registry = 'cicdrepotemp'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Build Docker Image') {
            agent any
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }
        } 
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        }
        stage('Deployed') { 
            steps { 
                sh "docker stop py"
                sh "docker rm py"
                sh "docker run -dt --name py -p 5000:5000 $registry:$BUILD_NUMBER" 
            }
        } 

    }
}
