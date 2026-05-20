pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
    steps {
        sh 'docker build --no-cache -t aswinvtk/github-pages-site .'
    }
}

        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f github-pages-site || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d --name github-pages-site -p 9090:80 aswinvtk/github-pages-site'
            }
        }
    }
}
