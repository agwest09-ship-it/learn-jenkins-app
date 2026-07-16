pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    echo '======= BEFORE BUILD ======='
                    npm ls -la
                    node --version
                    npm --version
                    npm ci  
                    npm run build
                    echo '======= AFTER BUILD ======='
                    ls -la
                '''
            }
        }
    }
}
