pipeline {
    agent any

    stages {
        stage('Cloner le repo') {
            steps {
                git 'git@github.com:vickydepicard/projet1-ci-cd-docker-jenkins.git'
            }
        }

        stage('Construire l\'image Docker') {
            steps {
                script {
                    docker.build('projet1_pract:dev', './docker/dev')
                }
            }
        }

        stage('Lancer le conteneur') {
            steps {
                sh '''
                    docker stop projet1_pract || true
                    docker rm projet1_pract || true
                    docker run -d --name projet1_pract -p 8080:80 projet1_pract:dev
                '''
            }
        }
    }
}

