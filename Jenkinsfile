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
                            #/usr/local/bin/docker run -d -p 5002:5000 --name webapp01 webapp1:latest
                            echo "run docker image app1"
                        ''' 
                    }
                }
                stage('Run webapp2'){
                    steps{
                        sh '''
                            #/usr/local/bin/docker run -d -p 5003:5000 --name webapp01 webapp2:latest
                            echo "run docker image app2"
                        ''' 
                    }
                }
            }
        }

        stage('check if apps are running'){
            parallel {
                stage('check app1'){
                    steps{
                        sh '''
                            #curl http://localhost:5002
                            echo "app1 running"
                        ''' 
                    }
                }
                stage('Run webapp2'){
                    steps{
                        sh '''
                            #curl http://localhost:5003
                            echo "app2 running"
                        ''' 
                    }
                }
            }
        }

        parameters {
        choice(
            choices: ['app1' , 'app2', 'both', 'none'],
            description: 'choose app to terminate',
            name: 'WHICH_APP')
        }
        stage('kill both apps based on choice'){
            when {
                expression {
                    WHICH_APP == "both"
                }
                steps {
                    sh '''
                        #docker stop webapp01
                        #docker rm -f webapp01
                        #docker stop webapp02
                        #docker rm -f webapp02
                        echo "both apps are terminated"
                    '''
                }
            }
        }
        stage('kill only app1 based on choice'){
            when {
                expression {
                    WHICH_APP == "app1"
                }
                steps {
                    sh '''
                        #docker stop webapp01
                        #docker rm -f webapp01
                        echo "app1 is now terminated"
                    '''
                }
            }
        }
        stage('kill only app2 based on choice'){
            when {
                expression {
                    WHICH_APP == "app2"
                }
                steps {
                    sh '''
                        #docker stop webapp02
                        #docker rm -f webapp02
                        echo "app2 is now terminated"
                    '''
                }
            }
        }
        stage('kill only app2 based on choice'){
            when {
                expression {
                    WHICH_APP == "none"
                }
                steps {
                    sh 'echo "No container terminated as option selected is none"'
                }
            }
        }
               
    
    }
}