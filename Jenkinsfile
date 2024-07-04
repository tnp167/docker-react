pipeline {
    agent any

    environment {
        AWS_REGION = 'eu-west-2'
        EB_APP_NAME = 'frontend'
        EB_ENV_NAME = 'Frontend-env'
        S3_BUCKET_NAME = 'elasticbeanstalk-eu-west-2-646681947524'
        S3_BUCKET_PATH = 'frontend'
        AWS_VERSION_LABEL_FORMAT = "-${BUILD_NUMBER}"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('tnp167/docker-react', '-f Dockerfile.dev .')
                    sh 'npm install'
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
        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
               script {
                    step([$class: 'AWSEBDeploymentBuilder',
                        credentialId: 'AWS_CREDENTIALS', 
                        awsRegion: "${env.AWS_REGION}",
                        applicationName: "${env.AWS_APPLICATION_NAME}",
                        environmentName: "${env.AWS_ENVIRONMENT_NAME}",
                        keyPrefix: "${env.S3_BUCKET_PATH}",
                        rootObject: ".",
                        versionLabelFormat: "${env.AWS_VERSION_LABEL_FORMAT}"
                    ])
                }
            }
        }
    }
}
