pipeline {
    agent any

    triggers {
        githubPush()
    }

    tools {
        maven 'Maven'
        jdk 'JDK17'
    }

    environment {
        DOCKER_IMAGE = "srikanthpalem/demo-app:latest"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/srikanthpalem/demo-app.git'
            }
        }

        stage('Build') {
            steps {
                bat 'java -version'
                bat 'mvn -version'
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat "echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin"
                    bat "docker push ${DOCKER_IMAGE}"
                }
            }
        }

        stage('Deploy to Kubernetes') {
    steps {
        bat 'kubectl apply -f deployment.yaml 
        bat 'kubectl apply -f service.yaml 
        bat 'kubectl rollout restart deployment demo-app-deployment'
    }

}
stage('Test K8s') {
    steps {
        bat 'kubectl get nodes'
    }
}

    }
}