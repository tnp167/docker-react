pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('tnp167/docker-react', '-f Dockerfile.dev .')
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('tnp167/docker-react').inside {
                        sh 'npm run test'
                    }
                }
            }
        }
    }
}