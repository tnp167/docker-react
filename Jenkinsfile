pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('tnp167/docker-react', '-f Dockerfile.dev .')
                    sh 'npm install'
                    sh 'npm run start'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('tnp167/docker-react').inside('-e CI=true') {
                        sh 'npm run test'
                    }
                }
            }
        }
    }
}
