pipeline {
    node('docker'){}
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
            stage('Build image') {
                /* This builds the actual image; synonymous to
                * docker build on the command line */

                def customImage = docker.build("was:${env.BUILD_ID}")
            }

        }

    }
}
