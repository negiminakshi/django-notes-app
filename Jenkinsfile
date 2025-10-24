pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                echo "cloning code from github"
                git url: "https://github.com/negiminakshi/django-notes-app.git", branch: "master"
            }
        }

        stage('build') {
            steps {
                script {
                    echo "login docker and build image"
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "docker login -u ${DOCKER_USER} -p ${DOCKER_PASS}"
                        sh " sudo docker build -t ${DOCKER_USER}/django-app ."
                    }
                }
            }
        }

        stage('test') {
            steps {
                echo "testing my code"
            }
        }

        stage('push to docker') {
            steps {
                script {
                    echo "pushing image into docker hub"
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "docker push ${DOCKER_USER}/django-app"
                    }
                }
            }
        }

        stage('deploy') {
            steps {
                echo "deploying my application"
                sh "docker compose up -d"
            }
        }
    }
}

