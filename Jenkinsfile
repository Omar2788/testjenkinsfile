pipeline {
    agent any
    environment {
        DOCKER_CREDS = credentials('docker')
        APP_NAME = 'storemanagement'
        DOCKER_REPO = "${DOCKER_CREDS_USR}/${APP_NAME}"
        IMAGE_TAG = "${BUILD_ID}-${BRANCH_NAME}"
        STOREMAN_IMAGE_NAME = "${DOCKER_REPO}:${IMAGE_TAG}"
    }

    stages {
        stage('Build Display build data') {
             steps {
                bat 'set'
             }
        stage('Build Artifact') {
            steps {
                powershell 'mvn clean package'
            }
        }
        stage('Build and Publish Image') {
               steps {
                   powershell "docker build --tag ${STOREMAN_IMAGE_NAME} ."
                   powershell "docker login -u ${DOCKER_CREDS_USR} -p ${DOCKER_CREDS_PSW}"
                   powershell "docker push ${STOREMAN_IMAGE_NAME}"
               }
           }
        stage('Deploy') {
            steps {
                powershell 'docker-compose up -d'
            }
        }
    }
}