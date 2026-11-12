pipeline {
    agent any
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
                sh 'npm install netlify-cli'
                sh 'node_mmodules/.bin/netlify --version'
            }
        }
    }

}