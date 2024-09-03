pipeline {
    agent any

    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                git ''
            }
        }

        stage('Git Checkout') {
            steps {
                echo 'Cloning the repository...'
                sh 'git@github.com:charleskiliya/CI-CD-With-Jenkins.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh './build.sh'  // Commande pour construire le projet
            }
        }

        stage('Unit Test') {
            steps {
                echo 'Running unit tests...'
                sh 'ansible-playbook unit_tests.yml'
            }
            post {
                always {
                    junit 'reports/*.xml'
                }
            }
        }

        stage('Integration Test') {
            steps {
                echo 'Running integration tests...'
                sh 'ansible-playbook integration_tests.yml'
            }
        }

        stage('Creating Database') {
            steps {
                echo 'Creating the database...'
                sh 'ansible-playbook create_database.yml'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh 'ansible-playbook deploy.yml'
            }
        }
    }

    post {
        always {
            echo 'Pipeline terminé !'
        }
    }
}
