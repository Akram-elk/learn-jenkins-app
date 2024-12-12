pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                agent {
                    docker {
                        image 'node:18-alpine'
                        reuseNode true
                    }
                }
                echo 'Hello World'
                sh'''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                 '''
            }
        }
    }
}
