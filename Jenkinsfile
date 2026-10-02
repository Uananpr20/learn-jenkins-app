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
                sh'''
                    ls -la
                    node --version
                    npm --version
                    npm ping
                    npm config get registry
                    npm config set strict-ssl false
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Staging') {
            steps {
                sh'''
                    ls -la
                    node --version
                    npm --version
                    npm config set strict-ssl false
                    npm ci
                    npm test
                    ls -la
                '''
            }
        }
    }
}
