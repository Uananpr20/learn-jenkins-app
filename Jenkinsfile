pipeline {
     agent {    
            docker {
                image 'node:18-alpine'
                reuseNode true
                args '-v /var/cache/jenkins-npm:/tmp/.npm'
            }
        }

        environment{
            CI = 'true'
            npm_config_cache = '/tmp/.npm'
        }

    stages {
        stage('Build') {    
            steps {
                sh'''
                    ls -la
                    node --version
                    npm --version
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
                    npm test
                '''
            }
        }
    }
}
