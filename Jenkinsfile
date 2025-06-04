pipeline {
    agent any

    tools {
        // You must configure this tool in Jenkins > Global Tool Configuration
        dependencyCheck 'Default' 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build steps here (e.g., `mvn clean install`)
            }
        }

        stage('Dependency Check') {
            steps {
                dependencyCheck additionalArguments: ''
            }
        }
    }

    post {
        always {
            node {
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
    }
}
