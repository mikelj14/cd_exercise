pipeline {

    agent {
        docker {
            image 'python:3.12'
            args '-u root'
        }
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh '''
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                pytest
                '''
            }
        }
    }
}
