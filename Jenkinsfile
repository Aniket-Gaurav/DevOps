pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t myflaskapp .'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 --name myflaskapp myflaskapp'
                    sh 'sleep 10' // wait for container to be ready
                    sh 'curl -f http://localhost:5000 || (docker logs myflaskapp && exit 1)'
                    sh 'docker stop myflaskapp'
                    sh 'docker rm myflaskapp'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // In a real scenario, deploy to a staging/production server
                    sh 'echo "Deploying..."'
                }
            }
        }
    }
}
