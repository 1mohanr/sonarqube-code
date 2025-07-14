pipeline {
    agent any

    environment {
        SONARQUBE = credentials('sonarqube-token')
    }

    stages {
        stage('Tool Install') {
            steps {
                tool name: 'Maven 3.8.1', type: 'maven'
            }
        }

        stage('Clone') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'https://github.com/1mohanr/sonarqube-code.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "No Maven build. Placeholder step."'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv(MySonarQube) {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=sonarqube-code -Dsonar.login=$SONARQUBE'
                }
            }
        }
    }
}
