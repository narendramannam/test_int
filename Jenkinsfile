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
                        sh '''
                        #/usr/local/bin/docker build -f Dockerfile_App1 . -t webapp1:latest
                        echo "build docker image app1"
                        ''' 
                    }
                }
                stage('build webapp2'){
                    steps{
                        sh '''
                        #/usr/local/bin/docker build -f Dockerfile_App2 . -t webapp2:latest
                        echo "build docker image app2"
                        '''
                    }
                }
            }
            
        }
        stage('run app1 and app2'){
            parallel {
                stage('Run webapp1'){
                    steps{
                        sh '''
                            #/usr/local/bin/docker run -d -p 5002:5000 -f webapp1:latest
                            echo "run docker image app1"
                        ''' 
                    }
                }
                stage('Run webapp2'){
                    steps{
                        sh '''
                            #/usr/local/bin/docker run -d -p 5003:5000 webapp2:latest
                            echo "run docker image app2"
                        ''' 
                    }
                }
            }
        }
    }
}