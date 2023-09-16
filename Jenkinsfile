pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker login -u shankar123321 -p $DOCKER_HUB_PASSWORD"
                    sh "docker build -t shankar123321/react-frontend:v1.${BUILD_ID} ."
                    sh 'docker tag shankar123321/react-frontend:latest'
                    sh "docker push shankar123321/react-frontend:v1.${BUILD_ID}"
                    sh 'docker push shankar123321/react-frontend:latest'
                    sh 'docker rmi shankar123321/react-frontend:v1.${BUILD_ID} shankar123321/react-frontend:latest"
                    
                }
            }
        }

        stage('docker run') {
            steps {
                script {
                  sh ' docker stop shankar123321/react-frontend'
                  sh ' docker rm -f shankar123321/react-frontend'
                  sh ' docker rmi shankar123321/react-frontend'
                  sh " docker run -d -p 3000:3000 shankar123321/react-frontend"
                }
            }
        }
    }

    post {
        success {
            // Notify or perform actions when the pipeline succeeds
            sh 'echo "Success"'
        }
        failure {
            // Notify or perform actions when the pipeline fails
            sh 'echo "Failed"'
        }
    }
}
