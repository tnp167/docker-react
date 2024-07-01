pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('test', '-f Dockerfile.dev .')
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('test').inside('-e CI=true') {
                        sh 'npm run test'
                    }
                }
            }
        }
    }
}
