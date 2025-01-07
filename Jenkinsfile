pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'echo "Building Stage"'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'echo "Testing Stage"'
                }
            }
        }
        stage('Package') {
            steps {
                script {
                    sh 'echo "Packaging Stage"'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh 'echo "Deploying Stage"'
                }
            }
        }
        stage('clean uo') {
            steps {
                script {
                    sh 'echo "cleaning up Stage"'
                }
            }
        }
    }
}
