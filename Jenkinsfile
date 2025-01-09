pipeline {
    agent any
    environment {
        DOCKER_CREDS = credentials('docker') // Récupère les identifiants Docker à partir des credentials Jenkins
        APP_NAME = 'storemanagement'
        DOCKER_REPO = "${DOCKER_CREDS_USR}/${APP_NAME}" // Nom du dépôt Docker
        IMAGE_TAG = "${BUILD_ID}-${BRANCH_NAME}" // Tag unique pour l'image Docker
        STOREMAN_IMAGE_NAME = "${DOCKER_REPO}:${IMAGE_TAG}" // Nom complet de l'image Docker avec tag
    }

    stages {
        stage('Display Build Data') {
            steps {
                bat 'set' // Affiche les variables d'environnement sous Windows
            }
        }
        stage('Build Artifact') {
            steps {
                powershell 'mvn clean package' // Compile le projet avec Maven
            }
        }
        stage('Build and Publish Image') {
            steps {
                powershell "docker build --tag ${STOREMAN_IMAGE_NAME} ." // Construit l'image Docker
                powershell "docker login -u ${DOCKER_CREDS_USR} -p ${DOCKER_CREDS_PSW}" // Authentification Docker
                powershell "docker push ${STOREMAN_IMAGE_NAME}" // Pousse l'image dans le dépôt Docker
            }
        }
        stage('Deploy') {
            steps {
                powershell 'docker-compose up -d' // Lance les conteneurs avec Docker Compose
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
        always {
            cleanWs() // Nettoie le workspace après l'exécution
        }
    }
}
