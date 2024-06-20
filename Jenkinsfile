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
                # Use a local cache directory
                npm config set cache ~/.npm-cache --global
                # Ensure permissions for the cache directory
                mkdir -p ~/.npm-cache && chown -R $(id -u):$(id -g) ~/.npm-cache
                rm -rf node_modules
                rm -f package-lock.json

                # Install dependencies
                npm install
                
                # Run the build
                npm run build
                
                ls -la
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Test Stage'
            }
        }
    }
}
