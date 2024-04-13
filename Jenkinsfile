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
                deploy adapters: [tomcat7(credentialsId: '5b05a0c0-612d-4742-9516-88bb4f80b9dc', path: '', url: 'http://localhost:8181/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
