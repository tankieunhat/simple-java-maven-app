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
        stage('Test-Plugin') {
            steps {
                sh 'exit 1'
                currentBuild.result = 'SUCCESS'
            } catch (any) {
                currentBuild.result = 'FAILURE'
                throw any
            } finally {
                step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'me@me.com', sendToIndividuals: true]])
            }
        }


    }
}