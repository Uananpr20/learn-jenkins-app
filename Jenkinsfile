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
                sh'''
                    ls -la
                    node --version
                    npm --version
                    npm ping
                    npm config get registry
                    npm config set strict-ssl false
                    npm install
                    npm run build
                    ls -la
                '''
            }
        }
    }
}
