pipeline {

    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/mikelj14/cd_exercise.git'
            }
        }


        stage('Install Dependencies') {
            steps {
                sh '''
                pip3 install -r requirements.txt
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
