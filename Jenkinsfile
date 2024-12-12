pipeline {
    agent any

    environment {
        NETLIFLY_SITE_ID = 'ae9ed7e3-32d9-4a4f-8c35-1aa2637b0ed9'
        NETLIFLY_AUTH_TOKEN = credentials('netlifly-token')
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Hello World'
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

        stage('test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps {
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }

                stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Hello World'
                sh '''
                    npm install netlify-cli
                    npm --version
                    echo "Deploying to production. Site ID: $NETLIFLY_SITE_ID"
                    node_modules/.bin/netlifly status
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