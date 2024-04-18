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
                        deploy adapters: [tomcat9(credentialsId: '2eab35d6-44ec-46f7-b4c2-a2d14660fe7b', path: '', url: 'http://localhost:8181/')], contextPath: null, war: '**/*.war'
                    }
        }
    }
}
