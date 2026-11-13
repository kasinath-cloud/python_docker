
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Getting code from GitHub'
                checkout scm
            }
        }

        stage('Verify') {
            steps {
                echo 'Checking project files'
                sh 'pwd'
                sh 'ls -la'
            }
        }
    }
}

