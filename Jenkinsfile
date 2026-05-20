pipeline {
    agent any

    environment {
        IMAGE_NAME = "yourdockerhubusername/myapp"
        CONTAINER_NAME = "myapp-container"
    }

    stages {

        stage('Clone') {
            steps {
                echo 'Cloning Repository'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Test') {
            steps {
                sh '''
                docker rm -f test-container || true

                docker run -d \
                --name test-container \
                -p 3000:3000 \
                $IMAGE_NAME

                sleep 10

                curl http://localhost:3000
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f production || true

                docker run -d \
                --name production \
                -p 80:3000 \
                $IMAGE_NAME
                '''
            }
        }
    }
}
