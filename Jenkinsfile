pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("my-docker-image")
                }
            }
        }
        stage('Test Docker Image') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'docker run --rm my-docker-image /app/path/to/your-windows-test-command.bat'
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') {
                        dockerImage.push('latest')
                    }
                }
            }
        }
        stage('Push Code to GitHub') {
            steps {
                sh 'git push origin master'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
