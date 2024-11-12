pipeline {
    agent any
    tools {
        maven 'local_maven'
    }
    stages {
        stage ('Build') {
            steps {
                sh 'mvn clean package'
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
                script {
                    try {
                        deploy adapters: [tomcat9(
                            credentialsId: 'Tomcat_Credentials',
                            path: '',  // Set to '' for root or specify context path
                            url: 'http://localhost:8090/'
                        )], contextPath: '', war: '**/*.war'
                    } catch (Exception e) {
                        echo "Deployment failed: ${e}"
                    }
                }
            }
        }
    }
}
