pipeline {
    agent any 
    tools {
        maven 'local_maven'
    }
    stages {
        stage ('Build') {
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps {
                deploy adapters: [tomcat7(credentialsId: '17548d75-b25d-497d-89d6-bb2255401774', path: '', url: 'http://localhost:8181/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
