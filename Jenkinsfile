pipeline {
    agent any

    stages {

        stage('Code') {
            steps {
                echo 'Récupération du code depuis GitHub...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Construction de l image Docker...'
                sh 'docker build -t devops-pipeline:latest .'
            }
        }

        stage('Test') {
            steps {
                echo 'Vérification de l image Docker...'
                sh 'docker images | grep devops-pipeline'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Déploiement du conteneur...'
                sh 'docker stop devops-app || true'
                sh 'docker rm devops-app || true'
                sh 'docker run -d --name devops-app -p 8085:80 devops-pipeline:latest'
                echo 'Application déployée sur http://localhost:8085'
            }
        }

    }

    post {
        success {
            echo 'Pipeline exécuté avec succès !'
        }
        failure {
            echo 'Erreur dans le pipeline !'
        }
    }
}
