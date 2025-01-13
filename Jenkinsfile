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
            sh '''
                php -v
                composer install
                cp .env.example .env
                php artisan key:generate
                php artisan migrate
            '''
        }
    }
        stage('Execute Tests') {
        steps {
            sh '''
                sed -i "s/^APP_KEY=.*/APP_KEY=$(php artisan key:generate --show)/" .env
                mkdir -p storage/framework/sessions
                mkdir -p storage/framework/cache
                mkdir -p storage/framework/views
                echo "APP_KEY Updated"
                echo "Running Tests"
                ./vendor/bin/phpunit --log-junit tests/junit.xml
            '''
        }
        
        post {
            always {
                junit 'tests/junit.xml'
            }
        }
    } 
    }
}