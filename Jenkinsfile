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
                powershell 'echo Build step goes'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                powershell 'echo Test step goes here'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                powershell 'echo Deploy step goes here'
            }
        }
    }

}
