pipeline {
    agent any
    stages {
        stage('Clone repository') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/KaloshevD/Jenkins-Pipeline-Labs.git',
                        credentialsId: 'github-creds'
                    ]]
                ])
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('kaloshev/nginx-demo:latest')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(
                        credentialsId: 'docker-creds',
                        url: 'https://index.docker.io/v1/'
                    ) {
                        docker.image('kaloshev/nginx-demo:latest').push()
                    }
                }
            }
        }
    }
}
