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
                    echo "======= BEFORE BUILD ======="
                    ls -la
                    node --version
                    npm --version
                    npm ci  
                    npm run build
                    echo "======= AFTER BUILD ======="
                    ls -la
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    test -f ./build/index.html
                    npm test
                '''
            }
        }
    }
}
