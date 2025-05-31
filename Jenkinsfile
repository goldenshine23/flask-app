pipeline {
    agent any

    environment {
        IMAGE_NAME = 'chinedudazi/my-image'
        CONTAINER_NAME = 'my-flaskapp'
    }

    stages {
        stage('Checkout') {
            steps {
                git(
                    url: 'https://github.com/goldenshine23/flask-app.git',
                    credentialsId: 'goldenshine23', // Ensure this ID exists in Jenkins credentials
                    branch: 'main'
                )
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    sh "docker run -d --name ${CONTAINER_NAME} -p 5000:5000 ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline complete.'
        }
    }
}
