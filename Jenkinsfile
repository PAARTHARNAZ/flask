pipeline {
    agent any

    environment {
        PYTHON_VERSION = '3.8'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning the GitHub repository...'
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/PAARTHARNAZ/flask.git',
                        credentialsId: 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 // Replace with your credentials ID
                    ]]
                ])
            }
        }

        stage('Setup Python Environment') {
            steps {
                echo 'Setting up Python environment...'
                sh '''
                    python3 -m venv venv
                    source venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                echo 'Running Unit Tests...'
                sh '''
                    source venv/bin/activate
                    pytest --maxfail=1 --disable-warnings -q
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh '''
                    source venv/bin/activate
                    python setup.py install
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh '''
                    source venv/bin/activate
                    # Add your deployment commands here
                    # e.g., gunicorn app:app
                '''
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'rm -rf venv'
        }
    }
}
