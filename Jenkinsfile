pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/Aniket-Gaurav/DevOps.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh './your-unix-build-command.sh'
                    } else {
                        bat 'path\\to\\your-windows-build-command.bat'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh './your-unix-test-command.sh'
                    } else {
                        bat 'path\\to\\your-windows-test-command.bat'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    if (isUnix()) {
                        sh './your-unix-deploy-command.sh'
                    } else {
                        bat 'path\\to\\your-windows-deploy-command.bat'
                    }
                }
            }
        }
    }
}
