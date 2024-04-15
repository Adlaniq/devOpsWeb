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
                deploy adapters: [tomcat7(credentialsId: '84a96ca3-d469-45cc-81b4-f8ef564ce54e', path: '', url: 'http://192.168.1.16:8181/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
