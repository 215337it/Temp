pipeline {
    agent any
    tools {
        maven 'local_maven'
    }
    stages {
        stage ('Build') {
            steps {
                bat 'mvn clean package' // Use 'bat' instead of 'sh' on Windows
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Tomcat Server') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'Tomcat_Credentials', path: '', url: 'http://localhost:8090/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
