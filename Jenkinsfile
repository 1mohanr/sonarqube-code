pipeline {
    agent any

    tools {
        maven 'Maven 3.8.1'
    }

    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/1mohanr/sonarqube-code.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}
