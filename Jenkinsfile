pipeline {

    agent any

    stages {

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
