pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Récupération du code depuis GitHub...'
                checkout scm
            }
        }

        stage('Install') {
            steps {
                echo 'Installation des dépendances...'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Lancement des tests...'
                sh 'npm test'
            }
        }

        stage('Build Docker') {
            steps {
                echo 'Construction de l image Docker...'
                sh 'docker build -t devops-tp-complet:latest .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Déploiement sur Kubernetes...'
                sh 'kubectl apply -f k8s/'
            }
        }
    }

    post {
        success {
            echo 'Pipeline terminé avec succès !'
        }
        failure {
            echo 'Le pipeline a échoué !'
        }
    }
}
