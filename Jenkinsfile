def sayHello(String name = 'human') {
  echo "Hello, ${name}."
  echo "Hello, ${name}."
}

pipeline {
    agent {label 'maven-label'}

    tools {
        maven "maven3.8.4"
    }

    stages {
        stage('Build') {
            steps {
                cleanWs()
                sayHello "DevOps Team"
                git branch: 'master', url: 'https://github.com/vytec-bs/myapp.git'                
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
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
