pipeline {
    agent any
    tools {
        maven '3.9.9'
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
    post{
        always {
            step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'winnhat2000@gmail.com', sendToIndividuals: true])
        }
    }
}