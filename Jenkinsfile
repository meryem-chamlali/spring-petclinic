pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9'
        jdk 'jdk1.8.0_151'
    }

    stages {

        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Compilation') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Tests Unitaires') {
            steps {
                bat 'mvn test'
            }

            post {
                always {
                    junit 'target/surefire-reports/**/*.xml'
                }
            }
        }

        stage('Couverture de code') {
            steps {
                bat 'mvn jacoco:report'
            }
        }

        stage('Documentation') {
            steps {
                bat 'mvn javadoc:javadoc'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn package'
            }
        }
    }
}
