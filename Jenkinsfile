pipeline {
    agent any

    tools {
        // Optional: if using Maven or Gradle
        // maven 'Maven 3.8.6'
    }

    environment {
        SONARQUBE_SERVER = 'My Sonar' // Must match the name from step 4
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    sh "sonar-scanner"
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
