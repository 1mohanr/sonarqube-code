pipeline {
    agent any

    environment {
        SONARQUBE = credentials('sonarqube-token')
    }

    stages {
        stage('Tool Install') {
            steps {
                tool name: 'maven', type: 'maven'
            }
        }

        stage('Clone') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'https://github.com/1mohanr/sonarqube-code.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "No build step (no Maven project)"'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "sonar-scanner -Dsonar.projectKey=sonarqube-code -Dsonar.sources=. -Dsonar.host.url=http://http://13.201.129.109:9000 -Dsonar.login=$SONARQUBE"
                }
            }
        }
    }
}
