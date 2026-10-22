pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'DevOpsFlow CI/CD Pipeline started'
                bat 'git --version'
                bat 'docker --version'
            }
        }

        stage('Validate Files') {
            steps {
                bat 'if not exist app\\index.html exit /b 1'
                bat 'if not exist app\\style.css exit /b 1'
                bat 'if not exist Dockerfile exit /b 1'
                echo 'All required project files are present'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devopsflow-dashboard:v1 .'
            }
        }

        stage('Verify Docker Image') {
            steps {
                bat 'docker image inspect devopsflow-dashboard:v1'
            }
        }
    }
        stage('Deploy Dashboard') {
            steps {
                bat 'docker rm -f devopsflow-dashboard || exit /b 0'
                bat 'docker run -d --name devopsflow-dashboard -p 8086:80 --restart unless-stopped devopsflow-dashboard:v1'
                echo 'Dashboard deployed successfully'
    }
}
    post {
        success {
            echo 'SUCCESS: DevOpsFlow pipeline completed'
        }
        failure {
            echo 'FAILED: Check the Jenkins console output'
        }
    }
}
