pipeline {
    agent any
    tools{
        gradle 'mygradle'
    }
    stages {
        stage('Build'){
            steps{
                sh 'gradle clean build'
            }
        }
        stage("CQA"){
            steps{
                script{
                def scannerHome = tool 'mysonar';
                withSonarQubeEnv('mysonar') {
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=myproject"
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
            steps{
            sh 'trivy  image medhasritha/adservice:latest'
            }
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
