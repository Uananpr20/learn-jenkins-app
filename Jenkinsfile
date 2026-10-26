pipeline {
   agent any

    stages {
        /*stage('Build') {    
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
        }*/

        stage('Test') {

            agent {    
                docker {
                    image 'node:18-alpine'
                    reuseNode true
            }
        }
            steps {
                sh '''
                    test -f build/index.html  && echo "file exist"
                    npm test
                '''
            }
        }


        stage('E2E') {

            agent {    
                docker {
                        image 'mcr.microsoft.com/playwright:v1.64.1-noble'
                        reuseNode true
            }
        }

            steps {
                sh'''
                    npm install serve
                    node_modules\.bin\serve -s build
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
