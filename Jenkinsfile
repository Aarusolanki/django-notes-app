pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Aarusolanki/django-notes-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t aartisolanki/django-notes:v1 .'
            }
        }

        stage('Run Docker') {
            steps {
                sh '''
                    docker stop django-app || true
                    docker rm django-app || true
                    docker run -d -p 8000:8000 --name django-app aartisolanki/django-notes:v1
                '''
            }
        }
    }
}

