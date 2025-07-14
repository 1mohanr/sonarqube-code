pipeline {
    agent any

    tools {
        maven 'Maven 3.8.1'
    }

    environment {
        PATH = "${tool 'Maven 3.8.1'}/bin:${env.PATH}"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/1mohanr/sonarqube-code.git'
            }
        }

        stage('Build') {
            steps {
                echo 'No Maven build. Placeholder step.'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'my-sonar-token', variable: 'SONARQUBE')]) {
                    withSonarQubeEnv('MySonarQube') {
                        sh """
                            sonar-scanner \\
                              -Dsonar.projectKey=sonarqube-code \\
                              -Dsonar.sources=. \\
                              -Dsonar.host.url=http://13.201.129.109:9000 \\
                              -Dsonar.login=$SONARQUBE
                        """
                    }
                }
            }
        }
    }
}
