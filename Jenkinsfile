pipeline {
    environment {
        registry = "raheelahmad20/cicd" 
       // registryCredential = 'dckr_pat_5vGIb5Fk16DmGoVdsR6NQ3h0f24' 
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

    }
}
