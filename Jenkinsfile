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

  /*  agent { 
        node('docker') { 
            stage('Test') {
                steps {
                    def customImage = docker.build("my-image:${env.BUILD_ID}")
                }
            }
        }
    }*/
}
