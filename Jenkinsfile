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
                    npm config set strict-ssl false
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            steps {
                sh'''
                    test -f build/index.html  && echo "file exist"
                    npm test
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
