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
                script {
                    echo 'Cleaning up the workspace...'
                    sh 'rm -rf $REPO_NAME $VENV_DIR'  // Remove old repo and virtual environment if they exist
                }
            }
        }
        stage('Clone Repository') {
            steps {
                script {
                    echo 'Cloning the Python project...'
                    sh 'git clone https://github.com/shafnajasir234/jenkinspyton.git'
                }
            }
        }
        stage('Setup Virtual Environment') {
            steps {
                script {
                    echo 'Creating Virtual Environment...'
                    // Create a new virtual environment
                    sh 'python3 -m venv $VENV_DIR'
                    
                    echo 'Installing Dependencies...'
                    // Activate the virtual environment and install the required dependencies
                    sh '. $VENV_DIR/bin/activate && pip install -r $REPO_NAME/requirements.txt'
                }
            }
        }
        stage('Run Application') {
            steps {
                script {
                    echo 'Starting the Python application...'
                    // Activate the virtual environment and start the app
                    sh '. $VENV_DIR/bin/activate && nohup python $REPO_NAME/app.py &'
                }
            }
        }
    }
}
