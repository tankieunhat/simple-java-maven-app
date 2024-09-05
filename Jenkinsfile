pipeline {
    agent any
    tools {
        mvn '3.9.9'
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}