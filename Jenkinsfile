pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Marcelosmbrrr/devops-cycle.git' 
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'composer install' 
            }
        }

        stage('Copy .env') {
            steps {
                sh 'cp .env.example .env || true'
            }
        }

        stage('Create SQLite Database') {
            steps {
                sh 'mkdir -p database && touch database/database.sqlite'
            }
        }

        stage('Set Permissions') {
            steps {
                sh 'chmod -R 775 storage bootstrap/cache'
            }
        }

        stage('Generate key') {
            steps {
                sh 'php artisan key:generate'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'php artisan test' 
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
