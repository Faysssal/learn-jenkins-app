pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = '2c1dc2e0-2b9a-46a4-9a93-9f9f22ede7a8'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }

    stages {
        stage('Build') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh 'npm ci'
                sh 'npm run build'
            }
        }
        
        stage('Test') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh 'test -f build/index.html'
                sh 'npm test'
            }
        }
        
        stage('Deploy') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh ''' 
                    sh 'npm install netlify-cli
                    sh './node_modules/.bin/netlify --version
                    sh 'echo "Deplyong to production, Site ID: $NETLIFY_SITE_ID"
                    sh './node_modules/.bin/netlify status
                    sh './node_modules/.bin/netlify deploy --dir=build --prod
                '''
            }
        }
    }

}