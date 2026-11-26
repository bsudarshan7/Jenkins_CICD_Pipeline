cat << 'EOF' > Jenkinsfile
pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/bsudarshan7/Jenkins_CICD_Pipeline'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-webapp:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop webapp || true'
                sh 'docker rm webapp || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name webapp -p 8080:80 devops-webapp:latest'
            }
        }

        stage('Deployment Check') {
            steps {
                sh 'docker ps'
                sh 'curl http://localhost:8080'
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
EOF
