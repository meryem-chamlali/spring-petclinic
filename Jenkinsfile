pipeline {
    agent any
    tools {
        maven 'Maven 3.9.9'
        jdk 'jdk1.8.0_151'
    }
    environment {
        MAVEN_OPTS = '-Dmaven.test.failure.ignore=false'
    }
    stages {
        stage('Scrutation SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
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
        stage('Analyse du code') {
            steps {
                bat 'mvn checkstyle:check'
            }
        }
        stage('Couverture de code') {
            steps {
                bat 'mvn jacoco:report'
            }
            post {
                always {
                    jacoco execPattern: 'target/jacoco.exec'
                }
            }
        }
        stage('JavaDoc') {
            steps {
                bat 'mvn javadoc:javadoc'
            }
        }
        stage('Rapport Web Maven Site') {
            steps {
                bat 'mvn site -DskipTests'
            }
        }
        stage('Packaging') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }
        stage('Deploiement Nexus') {
            steps {
                bat 'mvn deploy -DskipTests'
            }
        }
    }
    post {
        success {
            echo 'Build reussi'
            mail to: 'meryemchamlali7@gmail.com',
                 subject: 'BUILD JENKINS REUSSI',
                 body: 'Le pipeline a reussi !'
        }
        failure {
            mail to: 'meryemchamlali7@gmail.com',
                 subject: 'ECHEC DU BUILD JENKINS',
                 body: '''
Le pipeline Jenkins a echoue.
Projet : petclinic-pipeline
Consultez Jenkins pour voir l erreur.
'''
        }
    }
}
