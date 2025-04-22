pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6' // this name must match the name you configured in Jenkins → Global Tool Configuration
    }

    environment {
        SONARQUBE_SCANNER_HOME = tool 'SonarScanner' // must match the name you configured
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ramyamuddasani09/my-jenkins-project.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    sh 'mvn clean verify sonar:sonar'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
