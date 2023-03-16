pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }

    stages {
        stage('test01') {
            steps {
                echo 'Hello World'
            }
        }
        
    
    stage('Build') { 
            steps { 
                script{
                 /*sh 'docker build -t test01 .'*/
                 app = docker.build("test01")
                }
            }
        }
        
    
    stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://363412468025.dkr.ecr.us-east-2.amazonaws.com/test01', 'ecr:us-east-2:emoran') {
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
