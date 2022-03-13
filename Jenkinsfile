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
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                   sh "mvn -Dmaven.test.failure.ignore=true clean package sonar:sonar -Dsonar.host.url=https://sonarcloud.io -Dsonar.projectKey=vytec-bs_myapp -Dsonar.organization=vytec-bs -Dsonar.login=${SONAR_TOKEN}"
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
                }
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
