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
        echo "📦 Creating virtual environment"
        sh '''
            python3 -m venv venv
            source venv/bin/activate
            pip install --upgrade pip
            pip install -r requirements.txt
        '''
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

