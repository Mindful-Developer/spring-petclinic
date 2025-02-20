pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')
    }

    tools {
        maven 'Maven 3'
        jdk 'JDK 11'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Mindful-Developer/spring-petclinic.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Jacoco') {
            steps {
                sh 'mvn jacoco:prepare-agent test jacoco:report'
            }
            post {
                success {
                    jacoco execPattern: 'target/jacoco.exec'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
