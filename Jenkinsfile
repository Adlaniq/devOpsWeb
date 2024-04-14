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
                deploy adapters: [tomcat7(credentialsId: '5bea2314-3501-468e-9de4-ea20723c0d68', path: '', url: 'http://192.168.1.16:8181/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
