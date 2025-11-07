pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKERHUB_USERNAME = "srijoni08"
        IMAGE_NAME = "flask-cicd-demo"
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
