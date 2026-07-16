pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
        }
    }

    stages {
        stage('Build') {

            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci  
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            steps {
                echo "Test stage"
                sh '''
                    test -f ./build/index.html
                    npm test
                    npm install -g serve
                    serve -s build
                '''
            }
        }

        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.61.0-noble'
                    reuseNode true
                    arg '-u root:root'
                }
            }

            steps {
                sh '''
                    npm install serve
                    serve -s build
                    npx playwright test
                '''

            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
