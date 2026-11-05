pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS12', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://B363B9A309E242C130B76843B69EBCCC.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS12', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://B363B9A309E242C130B76843B69EBCCC.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
