
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out GitHub repository'
            }
        }

        stage('Check Python') {
            steps {
                bat 'py --version'
                bat 'where py'
            }
        }

        stage('Create Virtual Environment') {
            steps {
                bat 'py -m venv venv'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                    venv\\Scripts\\python.exe -m pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                bat '''
                    venv\\Scripts\\python.exe -m pytest tests/ -v --junitxml=test-results.xml
                '''
            }
            post {
                always {
                    junit allowEmptyResults: true,
                    testResults: 'test-results.xml'
                }
            }
        }

        stage('Build Complete') {
            steps {
                echo 'Flask Portfolio Build Completed!'
            }
        }
    }

    post {
        success {
            echo 'BUILD SUCCESSFUL!'
        }
        failure {
            echo 'BUILD FAILED!'
        }
    }
}
