pipeline{
    agent any 
    tools{
        maven 'local_maven'
    }
    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifcacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server'){
            step{
                deploy adapters: [tomcat7(credentialsId: '5bea2314-3501-468e-9de4-ea20723c0d68', path: '', url: 'http://localhost:8181/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
