pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t test -f Dockerfile.dev .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run -e CI=true test npm run test'
            }
        }
    }
}
