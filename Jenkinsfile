pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Apply Kubernetes manifests
                    sh 'kubectl apply -f k8s/deployment'
                    sh 'kubectl apply -f k8s/service'
                }
            }
        }
        
        stage('Deploy Prometheus and Grafana') {
            steps {
                script {
                    // Apply Prometheus and Grafana manifests
                    sh 'kubectl apply -f prometheus/prometheus.yaml'
                    sh 'kubectl apply -f prometheus/prometheus-service.yaml'
                    sh 'kubectl apply -f k8s/deployment/grafana-deployment.yaml'
                    sh 'kubectl apply -f k8s/service/grafana-service.yaml'
                }
            }
        }
    }
}
