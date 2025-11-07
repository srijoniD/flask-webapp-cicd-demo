pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKERHUB_USERNAME = "srijoni08"
        IMAGE_NAME = "flask-cicd-demo"
        AWS_CREDENTIALS = credentials('aws-credentials')  // Kind: Username with password
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/srijoniD/flask-webapp-cicd-demo.git',
                    credentialsId: 'github-token'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $DOCKERHUB_USERNAME/$IMAGE_NAME:latest .
                '''
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh '''
                echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
                docker push $DOCKERHUB_USERNAME/$IMAGE_NAME:latest
                '''
            }
        }

        stage('Deploy to EKS using Ansible') {
            steps {
                sh '''
                export AWS_ACCESS_KEY_ID=$AWS_CREDENTIALS_USR
                export AWS_SECRET_ACCESS_KEY=$AWS_CREDENTIALS_PSW
                export AWS_DEFAULT_REGION=us-east-1

                ansible-playbook ansible/deploy.yml
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Pipeline Failed!"
        }
    }
}
