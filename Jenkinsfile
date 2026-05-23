pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.host.url=http://sonarqube:9000' -Dsonar.token=sqa_f6606121ead2fb6a94935726323d3688d4234b09
            }
        }

        stage('Upload to Nexus') {
            steps {
                sh 'mvn deploy -DskipTests'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
