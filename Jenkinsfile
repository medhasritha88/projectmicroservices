pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS13', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://220096991BBABC3CEA2A458EBE694E8C.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS13', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://220096991BBABC3CEA2A458EBE694E8C.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
