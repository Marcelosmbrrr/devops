pipeline {
    agent any

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
    }

    post {
        success {
            echo "Successfully deployed to the main branch!"
        }
        failure {
            echo "There was an error deploying to the main branch."
        }
    }
}
