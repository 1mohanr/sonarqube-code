pipeline {
    agent any

    tools {
        maven 'Maven 3.8.1' // Make sure this exists in Jenkins Global Tool Configuration
    }

    environment {
        SONARQUBE = credentials('sonarqube-token') // Replace with your actual SonarQube Jenkins credentials ID
    }

    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/1mohanr/sonarqube-code.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Skipping Maven build step - no pom.xml"' // ✅ Dummy step
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    sh 'echo "Running SonarQube analysis..."'
                    sh 'mvn sonar:sonar -Dsonar.login=$SONARQUBE'
                }
            }
        }
    }
}
