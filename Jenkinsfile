pipeline {
    agent {
        node {
            label 'master'
        }
    }

    stages {
        stage('build dockerimage'){
            parallel {
                stage('build webapp1'){
                    steps{
                        sh 'docker build -f Dockerfile_App1 . -t webapp1:latest' 
                    }
                }
                stage('build webapp2'){
                    steps{
                        sh 'docker build -f Dockerfile_App2 . -t webapp2:latest' 
                    }
                }
            }
            
        }
        stage('run app1 and app2'){
            parallel {
                stage('Run webapp1'){
                    steps{
                        sh 'docker run -d -p 5002:5000 -f webapp1:latest' 
                    }
                }
                stage('Run webapp2'){
                    steps{
                        sh 'docker run -d -p 5003:5000 webapp2:latest' 
                    }
                }
            }
        }
    }
}