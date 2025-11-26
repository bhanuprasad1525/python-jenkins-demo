pipeline {
    agent any
 
    environment {
        VENV = 'venv'
        PYTHONPATH = '.'
    }
 
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
 
        stage('Setup Virtual Environment') {
            steps {
                bat """
                    python -m venv %VENV%
                    call %VENV%\\Scripts\\activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                """
            }
        }
 
        stage('Run Tests') {
            steps {
                bat """
                    call %VENV%\\Scripts\\activate
                    set PYTHONPATH=.
                    pytest tests
                """
            }
        }
    }
 
    post {
        success {
            echo "Tests passed!"
        }
        failure {
            echo "Tests failed!"
        }
    }
}