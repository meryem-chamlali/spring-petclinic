pipeline {
    agent any
    tools {
      maven 'Maven 3.9.9'
        jdk 'jdk1.8.0_151'
    }
    stages {

        stage ('Build') {
            steps {
                bat 'mvn install'
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml'
                }
            }
        }
    }
}
