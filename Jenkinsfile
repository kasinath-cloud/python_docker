pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Getting latest code from GitHub'
                checkout scm
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Django application to EC2'

                sh '''
                    ssh -i "$HOME/.ssh/ec2_deploy" \
                    -o IdentitiesOnly=yes \
                    -o BatchMode=yes \
                    ubuntu@172.31.20.31 '
                        set -e
                        cd /home/ubuntu/python_docker
                        git pull --ff-only origin main
                        sudo docker build -t python-docker-app:latest .
                        sudo docker rm -f python-django || true
                        sudo docker run -d --name python-django -p 8000:5005 python-docker-app:latest
                        curl -fsS http://localhost:8000/ > /dev/null
                    '
                '''
            }
        }
    }
}

