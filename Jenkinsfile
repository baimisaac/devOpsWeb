pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deploy to tomcat server'){
                    steps {
                        deploy adapters: [tomcat9(credentialsId: '35f3ace2-754d-401e-9055-c9b3b9960ff3', path: '', url: 'http://localhost:8181/')], contextPath: '/devOpsWeb, war: '**/*.war'
                    }
        }
    }
}
