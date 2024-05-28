pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'my-docker-image' // Change to your desired Docker image name
        REGISTRY_CREDENTIALS = 'dockerhub-credentials' // Credentials ID for Docker registry
    }
    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/Aniket-Gaurav/DevOps.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker build -t $DOCKER_IMAGE .'
                    } else {
                        bat 'docker build -t %DOCKER_IMAGE% .'
                    }
                }
            }
        }
        stage('Test Docker Image') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker run --rm $DOCKER_IMAGE your-unix-test-command.sh'
                    } else {
                        bat 'docker run --rm %DOCKER_IMAGE% path\\to\\your-windows-test-command.bat'
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', REGISTRY_CREDENTIALS) {
                        docker.image(DOCKER_IMAGE).push('latest')
                    }
                }
            }
        }
        stage('Push Code to GitHub') {
            steps {
                script {
                    // Pull latest changes
                    if (isUnix()) {
                        sh 'git pull origin master'
                    } else {
                        bat 'git pull origin master'
                    }

                    // Push changes to remote
                    if (isUnix()) {
                        sh 'git push origin master'
                    } else {
                        bat 'git push origin master'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker run -d --name my-app -p 80:80 $DOCKER_IMAGE'
                    } else {
                        bat 'docker run -d --name my-app -p 80:80 %DOCKER_IMAGE%'
                    }
                }
            }
        }
    }
    post {
        always {
            script {
                if (isUnix()) {
                    sh 'docker system prune -f'
                } else {
                    bat 'docker system prune -f'
                }
            }
        }
        cleanup {
            cleanWs()
        }
    }
}
