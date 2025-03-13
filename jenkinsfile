pipeline {
    agent any

    environment {
        SERVER_IP = "13.203.74.90"
        USER = "ubuntu"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/nadia-sultana2228/frontend-app.git', 
                    credentialsId: 'github-credentials'  // Add your credentials ID here
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy to Nginx') {
            steps {
                sh """
                ssh -o StrictHostKeyChecking=no $USER@$SERVER_IP '
                sudo rm -rf /var/www/html/*
                sudo cp -r dist/* /var/www/html/
                sudo systemctl restart nginx
                '
                """
            }
        }
    }
}
