pipeline {
    agent any

    environment {
        // Définir les variables d'environnement nécessaires
        APP_NAME = 'mon-application'
        DOCKER_IMAGE = 'mon-image-docker'
    }

    stages {
        stage('Checkout') {
            steps {
                // Cloner le dépôt Git
                git 'git@github.com:jozlk/Jenkins-CI-CD.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    // Exemple pour construire une application Java avec Maven
                    sh 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Exemple pour exécuter les tests unitaires avec Maven
                    sh 'mvn test'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Construire une image Docker
                    sh "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Pousser l'image Docker vers un registre Docker (ex. Docker Hub)
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                        sh "docker push ${DOCKER_IMAGE}"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Exemple de déploiement avec Ansible
                    sh 'ansible-playbook -i inventory/production deploy.yml'
                }
            }
        }
    }

    post {
        success {
            // Actions à effectuer si le pipeline réussit
            echo 'Le pipeline a réussi !'
        }
        failure {
            // Actions à effectuer si le pipeline échoue
            echo 'Le pipeline a échoué.'
        }
    }
}

