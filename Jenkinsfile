pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS13', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://8533B1DE90899826229D7D99BB8C86E4.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS13', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://8533B1DE90899826229D7D99BB8C86E4.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
