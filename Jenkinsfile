/*
pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
                
            }
        }
    }

    agent {
        // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
        dockerfile {
            filename 'Dockerfile'
            dir 'build'
            //label 'my-defined-label'
            additionalBuildArgs  '-t my-image:${env.BUILD_ID}'
            //args '-v /tmp:/tmp'
        }
    }

  / agent { 
        node('docker') { 
            stage('Test') {
                steps {
                    def customImage = docker.build("my-image:${env.BUILD_ID}")
                }
            }
        }
    }
}
*/

pipeline {
    agent none
    stages {
        stage('Back-end') {
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v /root/.m2:/root/.m2'
                }
            }
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Front-end') {
            agent any /*{
                dockerfile {
                    filename 'Dockerfile'
                    //dir 'build'
                    label 'my-defined-label:${env.BUILD_ID}'
                    //additionalBuildArgs  '-t my-image:${env.BUILD_ID}'
                    //args '-v /tmp:/tmp'
                }
            }*/
            steps {
                echo 'Hello World'
                def customImage = docker.build("my-image:${env.BUILD_ID}")
            }
        }
    }
}

/*
pipeline {
    agent none
    stage ('Checkout') {
        agent any
        steps {
            git(
                url: 'https://www.github.com/...',
                credentialsId: 'CREDENTIALS',
                branch: "develop"
            )
        }
    }
    stage ('Build') {
        agent {
            dockerfile {
            filename 'Dockerfile.ci'
        }
        steps {
            [...]
        }
}
    }
    [...]
}*/