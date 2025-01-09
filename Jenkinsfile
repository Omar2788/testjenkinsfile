pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'echo Build step goes here'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo Test step goes here'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh 'echo Deploy step goes here'
            }
        }
    }

}
