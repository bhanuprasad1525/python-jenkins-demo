pipeline {
    agent any

    environment {
        APP_NAME = 'python-jenkins-demo'
        VENV_DIR = 'venv'
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
                sh '''
                    python3 --version
                    python3 -m venv $VENV_DIR
                    . $VENV_DIR/bin/activate        # <-- FIXED
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . $VENV_DIR/bin/activate
                    export PYTHONPATH=$PYTHONPATH
                    pytest tests/
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}