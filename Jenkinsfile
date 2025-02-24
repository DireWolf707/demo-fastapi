pipeline {
    agent any

    environment {
        CONTAINER_ENVIRONMENT = "python:3.12-alpine"
        CONTAINER_PORT = "8000"
        HOST_PORT = "3001"
    }

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    runContainer("python -m venv .venv")
                    runContainer("source .venv/bin/activate && pip install -r requirements.txt")
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    deployContainer("source .venv/bin/activate && fastapi run main.py")
                }
            }
        }

        stage('Cloudflared Tunnel') {
            steps {
                script {
                    configureTunnel()
                }
            }
        }

    }
}
