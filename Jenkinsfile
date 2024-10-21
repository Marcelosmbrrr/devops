pipeline {
    agent any
    
    environment {
        SSH_KEY = credentials('ssh-key-id') 
        APP_DIR = '/path/production' 
        HOST = 'user@prod_domain.com' 
    }

    stages {

        // Jenkins Runner/Agent 

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Marcelosmbrrr/devops-cycle.git' 
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'composer install --no-dev' 
            }
        }

        stage('Run Tests') {
            steps {
                sh 'php artisan test' 
            }
        }

        stage('Run Migrations') {
            steps {
                sh 'php artisan migrate --force' 
            }
        }

        stage('Optimize Application') {
            steps {
                sh 'php artisan optimize'
            }
        }

        // Server Deployment

        stage('Deploy to Host') {
            steps {
                sshagent (credentials: ['ssh-key-id']) {
                    sh "rsync -avz --delete ./ ${HOST}:${APP_DIR}" 
                    sh "ssh ${HOST} 'cd ${APP_DIR} && php artisan storage:link'" 
                }
            }
        }
        
    }

    post {
        success {
            echo "Deploy realizado com sucesso na branch main!"
        }
        failure {
            echo "Houve um erro no deploy na branch main."
        }
    }
}
