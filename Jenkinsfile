pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build tool command here (e.g., sh 'mvn clean install')
            }
        }

        stage('Dependency Check') {
            steps {
                dependencyCheck odcInstallation: 'Default',
                                stopBuild: false
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
