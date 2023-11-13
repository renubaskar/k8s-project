pipeline {
    agent any
    stages {   
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/renubaskar/k8s-project.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t kubesimage /var/lib/jenkins/workspace/k8s-project-13'
                sh 'sudo docker tag kubesimage renubaskar7/kubesimage:latest'
                sh 'sudo docker tag kubesimage renubaskar7/kubesimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push renubaskar7/kubesimage:latest'
                sh 'sudo docker image push renubaskar7/kubesimage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/k8s-project-13/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
      
