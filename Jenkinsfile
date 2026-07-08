pipeline {
    agent any
    
    environment {
        IMAGE_NAME = 'my-flask-app'
        IMAGE_TAG  = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Build Initial Docker Image') {
            steps {
                script {
                    echo "Building temporary/latest Docker image for testing..."
                    sh "docker build --no-cache -t ${IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Run Unit Tests in Container') {
            steps {
                script {
                    echo "Running unit tests inside the container..."
                    sh "docker run --rm ${IMAGE_NAME}:latest python -m unittest test_app.py"
                }
            }
        }

        stage('Final Build & Tag (PR to Main Only)') {
            when {
                expression { env.CHANGE_ID != null && env.CHANGE_TARGET == 'main' }
            }
            steps {
                script {
                    echo "Pull Request detected targeting 'main'. Tagging official image: ${IMAGE_NAME}:${IMAGE_TAG}..."
                    sh "docker tag ${IMAGE_NAME}:latest ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage('Notify GitHub Success') {
            steps {
                script {
                    echo "Notifying GitHub that the build and tests have passed..."
                    githubNotify status: 'SUCCESS', description: 'Build and Tests Passed!', context: 'cd_practise_multy'
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            script {
                githubNotify status: 'FAILURE', description: 'Build Failed!', context: 'cd_practise_multy'
            }
            echo 'Pipeline failed. Status sent to GitHub as FAILURE.'
        }
    }
}