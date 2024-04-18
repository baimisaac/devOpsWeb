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
                        deploy adapters: [tomcat9(credentialsId: '6d527977-82c8-4059-973f-c390dc4fb23d', path: '', url: 'http://localhost:8181/')], contextPath: '/devOpsWeb', war: '**/*.war'
                    }
        }
    }
}
