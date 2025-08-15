pipeline {
    agent any
    environment {
        DOCKER_HUB_USER = "abhiramuujjaini"
        DOCKER_HUB_PASS = credentials('dockerhub-credentials-id')
    }
    stages {
        stage('Build & Push Frontend') {
            steps {
                dir('learnerReportCS_frontend') {
                    script {
                        sh """
                        docker login -u $DOCKER_HUB_USER -p $DOCKER_HUB_PASS
                        docker build -t $DOCKER_HUB_USER/herovired-frontend:latest .
                        docker push $DOCKER_HUB_USER/herovired-frontend:latest
                        """
                    }
                }
            }
        }
        stage('Build & Push Backend') {
            steps {
                dir('learnerReportCS_backend') {
                    script {
                        sh """
                        docker login -u $DOCKER_HUB_USER -p $DOCKER_HUB_PASS
                        docker build -t $DOCKER_HUB_USER/herovired-backend:latest .
                        docker push $DOCKER_HUB_USER/herovired-backend:latest
                        """
                    }
                }
            }
        }
        stage('Deploy with Helm') {
            steps {
                script {
                    sh """
                    helm upgrade --install mern-stack .container-orchestration-chart \
                        --set apps[0].image=$DOCKER_HUB_USER/mern-frontend:latest \
                        --set apps[1].image=$DOCKER_HUB_USER/mern-backend:latest
                    """
                }
            }
        }
    }