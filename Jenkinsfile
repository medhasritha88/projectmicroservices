pipeline {
    agent any

    stages {
        stage("CQA"){
            steps{
                script{
                def scannerHome = tool 'mysonar';
                withSonarQubeEnv('mysonar') {
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=myproject -Dsonar.project -Dsonar.sources=cartservice"
                }
            }
        }
    }
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    dir('src') {

                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t medhasritha/cartservice:latest ."
                    }
                        }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push medhasritha/cartservice:latest "
                    }
                }
            }
        }
    }
}
