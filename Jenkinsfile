pipeline {
    agent any

    environment {
        IMAGE_NAME = 'chinedudazi/my-image'
        CONTAINER_NAME = 'my-flaskapp'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your GitHub repo with credentials (replace credentialId accordingly)
                git(
                    url: 'https://github.com/goldenshine23/flask-app.git',
                    credentialsId: 'github-pat-credential-id',
                    branch: 'main'
                )
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
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
