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
                    test -f build/index.html  && echo "file exist I think"
                    npm test
                '''
            }
        }


        stage('E2E') {

            agent {    
                docker {
                        image 'mcr.microsoft.com/playwright:v1.39.0'
                        reuseNode true
            }
        }

            steps {
                sh'''
                    npm install serve
                    node_modules/.bin/serve -s build &
                    sleep 30
                    npx playwright test --reporter=html
                '''
            }
        }
    }


    post {
        always {
                junit 'jest-results/junit.xml'
        }
    }

}
