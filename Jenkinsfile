pipeline {
    agent any

    stages {
        stage('W/O Docker') {
            steps {
                sh 'echo "Without docekr'
            }
        }

        stage('W/ Docker') {
            agent {
                image: node:18-alpine
            }
            
            steps {
                sh 'echo "With docekr"'
            }
        }
    }
}