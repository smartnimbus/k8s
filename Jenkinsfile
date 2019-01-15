pipeline {
    agent none
    stages {
        stage('Package Application') {
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v /root/.m2:/root/.m2'
                }
            }
            steps {
                echo 'Hello Amit'
                sh 'mvn --version'
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Build Was Image') {
            agent any 
            steps {
                echo 'Hello World'

                script {
                    def customImage = docker.build("was8:${env.BUILD_ID}")
                }
            }
        }      
        stage('Run image') {
            agent any 
            steps {
                script {
                    /* Ideally, we would run a test framework against our image.
                    * For this example, we're using a Volkswagen-type approach ;-) */

                    //docker.image("was8:${env.BUILD_ID}").withRun("--name was8-${env.BUILD_ID} -p 9043:9043 -p 9443:9443 -d" ) {
                    sh "docker run --name was8-${env.BUILD_ID} -p 9043:9043 -p 9443:9443 -d was8:${env.BUILD_ID}"
                    sh "docker exec was8-${env.BUILD_ID} cat /tmp/PASSWORD"
                    //sh 'cat /tmp/PASSWORD'
                }
            }
        }
    }
}


