pipeline {
    agent any
    stages {
        stage('Initial Cleanup') {
            steps {
                dir("${WORKSPACE}") {
                    deleteDir()
                }
            }
        }
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Prince-Tee/php-todo.git'
            }
        }
        stage('Prepare Dependencies') {
            steps {
                script {
                    // Move .env.sample to .env and set environment variables
                    sh '''
                        mv .env.sample .env
                        echo "APP_KEY=" >> .env
                        echo "DB_HOST=${DB_HOST}" >> .env
                        echo "DB_PORT=${DB_PORT}" >> .env
                        echo "DB_DATABASE=${DB_DATABASE}" >> .env
                        echo "DB_USERNAME=${DB_USERNAME}" >> .env
                        echo "DB_PASSWORD=${DB_PASSWORD}" >> .env
                    '''
                    
                    // Create bootstrap cache directory with appropriate permissions
                    sh '''
                        mkdir -p bootstrap/cache
                        chown -R jenkins:jenkins bootstrap/cache
                        chmod -R 775 bootstrap/cache
                    '''
                    
                    // Install Composer dependencies with error handling
                    sh '''
                        set -e
                        composer install --no-scripts
                    '''
                    
                    // Run Laravel artisan commands
                    sh '''
                        php artisan key:generate
                        php artisan clear-compiled
                        php artisan migrate --force
                        php artisan db:seed --force
                    '''
                }
            }
        }
        stage ('Execute Unit Tests') {
            steps {
               // sh './vendor/bin/phpunit'                
            }
        } 
    }
}