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
                sh '''
                ls -la
                node --version
                npm --version
                npm cache clean --force
                rm -rf node_modules
                rm -f package-lock.json
                npm ci
                npm run build
                ls -la
                '''
            }
        }
    }
}
