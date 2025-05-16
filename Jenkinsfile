pipeline {
    agent any
    environment {
        PYTHON_HOME = "/usr/bin/python3"
        VENV_DIR = "venv"
        REPO_NAME = "jenkinspyton"
    }
    stages {
        stage('Clean Workspace') {
            steps {
                echo 'Cleaning up the workspace...'
                sh 'rm -rf $REPO_NAME $VENV_DIR'
            }
        }
        stage('Clone Repository') {
            steps {
                echo 'Cloning the Python project...'
                sh 'git clone https://github.com/shafnajasir234/jenkinspyton.git'
            }
        }
        stage('Setup Virtual Environment') {
            steps {
                echo 'Creating Virtual Environment...'
                sh 'python3 -m venv $VENV_DIR'
                
                echo 'Installing Dependencies...'
                sh '. $VENV_DIR/bin/activate && pip install --upgrade pip'
                sh ". $VENV_DIR/bin/activate && pip install -r $REPO_NAME/requirements.txt"
            }
        }
        stage('Run Flask Application') {
            steps {
                echo 'Starting the Flask application in background with logging...'
                sh """
                    . $VENV_DIR/bin/activate && \
                    nohup python $REPO_NAME/app.py > flask_app.log 2>&1 &
                """
            }
        }
        stage('Verify Flask Application') {
            steps {
                echo 'Checking if Flask app started successfully...'
                // Sleep for a few seconds to allow app to start
                sh 'sleep 5'
                // Check if the app.py process is running
                sh "ps aux | grep '[a]pp.py' || echo 'Flask app is not running'"
                // Optional: Show last 10 lines of the log file for debugging
                sh 'tail -n 10 flask_app.log || echo "No log file found"'
            }
        }
    }
}
