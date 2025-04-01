pipeline {
    agent any

    environment {
        PYTHON_VERSION = "3.10"
        VENV_DIR = "venv"
        SHELL = "/bin/bash" // Ensure Bash is used for shell commands
    }

    stages {
        stage('Checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/hruthingali/python-exam.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh 'python3 -m venv ${VENV_DIR}'
                sh 'bash -c "source ${VENV_DIR}/bin/activate && pip install --upgrade pip"'
                sh 'bash -c "source ${VENV_DIR}/bin/activate && pip install -r requirements.txt"'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'bash -c "source ${VENV_DIR}/bin/activate && pytest test_app.py"'
            }
        }

        stage('Build and Archive') {
            steps {
                sh 'mkdir -p build'
                sh 'cp app.py build/'
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
