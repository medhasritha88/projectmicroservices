pipeline {
    agent any
    

    stages {
        stage("CQA"){
            steps{
                script{
                def scannerHome = tool 'mysonar';
                withSonarQubeEnv('mysonar') {
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=myproject -Dsonar.sources=src/"
                }
            }
        }
    }

        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t medhasritha/adservice:latest ."
                    }
                }
            }
        }
        stage('Image Scanner'){
            sh 'trivy docker image medhasritha/adservice:latest'
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push medhasritha/adservice:latest "
                    }
                }
            }
        }
    }
}
