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
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test'){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm run test
                    if [ -f build/index.html ]; then
                      echo "build/index.html exists"
                    else
                      echo "build/index.html NOT FOUND" >&2
                      exit 1
                    fi
                    ls -la
                ''' 
            }
        }
    }
}
