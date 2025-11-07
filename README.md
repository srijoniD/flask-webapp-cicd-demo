This project demonstrates a complete CI/CD pipeline for deploying a Flask application to Amazon EKS (Kubernetes) using Jenkins, Docker, Ansible, and GitHub.

It shows how a simple application can be automatically built, containerized, pushed to DockerHub, and deployed to Kubernetes, without any manual steps.

Technologies Used-

- Flask (Python Web App)
- GitHub (Source Code Management)
- Jenkins (CI/CD Automation)
- Docker (Build and package app)
- DockerHub (Image registry)
- Ansible (Deployment automation)
- Amazon EKS (Managed Kubernetes cluster)
- kubectl & eksctl (Cluster operations)

Project Architecture Explained-

- Developer pushes code → GitHub
- Jenkins Pipeline triggers:
- Pulls latest code
- Builds Docker image
- Pushes image to DockerHub
- Runs Ansible to deploy the app-
- Ansible updates kubeconfig & applies manifests
- Kubernetes (EKS) runs the Flask application
- LoadBalancer URL exposes the app on the internet

CI/CD Pipeline Stages:-
1. Checkout Code
      Jenkins pulls the latest code from your GitHub repository.

2. Build Docker Image
      The Flask app is containerized using a Dockerfile.

3. Push to DockerHub
      The built image is pushed to your DockerHub repository.

4. Deploy to AWS EKS
     Ansible:
      Sets AWS credentials
      Updates kubeconfig
      Applies Kubernetes Deployment and Service YAMLs

5. Access the Application

Kubernetes creates an AWS LoadBalancer:
The Flask app becomes publicly accessible via the external URL.

  <img width="1016" height="368" alt="Web Browser Output" src="https://github.com/user-attachments/assets/a98d18ac-60b1-4da7-bb71-835e9652a0e6" />

  <img width="1016" height="368" alt="Jenkins Console Output - part 1" src="https://github.com/user-attachments/assets/e3fa9a90-c367-4846-adda-34d575d9f85d" />

  <img width="1760" height="775" alt="Jenkins Console Output- part 2" src="https://github.com/user-attachments/assets/fc8ef0f1-9942-4843-b9b9-31c60a6e933f" />


