pipeline {
    agent any

    environment {
        IMAGE_NAME = "notesapp:${BUILD_NUMBER}"
    }

    stages {
        stage('Clone Repo') {
            steps {
                checkout scm
                echo "✅ Code Cloned!"
            }
        }

        stage('Install Python Deps') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 $IMAGE_NAME'
            }
        }
    }

    post {
        success {
            echo "✅ CI/CD Completed Successfully!"
        }
        failure {
            echo "❌ CI/CD Failed. Check logs."
        }
    }
}

