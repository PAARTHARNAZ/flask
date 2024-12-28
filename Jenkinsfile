pipeline {
    agent any

    environment {
        // Environment variables for Python version and virtual environment path
        PYTHON_VERSION = '3.8'
        VENV_PATH = '.venv'
    }

    triggers {
        // Automatically trigger the pipeline when changes are pushed to GitHub
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning the GitHub repository...'
                git 'https://github.com/your-username/flask.git' // Replace with your forked repo link
            }
        }

        stage('Setup Python Environment') {
            steps {
                script {
                    echo 'Setting up Python virtual environment...'
                    // Set up virtual environment and install dependencies
                    sh """
                    python${PYTHON_VERSION} -m venv ${VENV_PATH}
                    source ${VENV_PATH}/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                    """
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    echo 'Running unit tests...'
                    sh """
                    source ${VENV_PATH}/bin/activate
                    pytest
                    """
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building the Flask app...'
                    // Add any build-related tasks here (e.g., packaging)
                    echo 'No specific build tasks needed for this Flask app.'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying the Flask app...'
                    // Deploy to your environment (e.g., SCP to server, Docker, or local setup)
                    sh """
                    source ${VENV_PATH}/bin/activate
                    python app.py &
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}
