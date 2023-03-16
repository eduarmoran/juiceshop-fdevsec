pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }

        stage('Build') { 
            steps { 
                script{
                 app = docker.build("pod-shopping")
                }
            }
        }
        
        
        stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://363412468025.dkr.ecr.us-east-2.amazonaws.com/pod-shopping', 'ecr:us-east-2:emoran') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
        stage('Deploy'){
            steps {
                 sh 'kubectl apply -f deployment.yml'
            }
        }
        
        
    }
}
