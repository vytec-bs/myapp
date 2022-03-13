@Library('pipeline-library-demo')_
pipeline {
    agent {label 'maven-label'}

    tools {
        maven "maven3.8.4"
    }

    stages {
        stage('Build') {
            steps {
                cleanWs()
                sayHello 'jenkins'
                git branch: 'master', url: 'https://github.com/vytec-bs/myapp.git'                
                sh "mvn -Dmaven.test.failure.ignore=true clean package org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=vytec-bs_myapp"
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
