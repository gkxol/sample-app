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
                // Add build tool commands here
                // For example: sh 'mvn clean install'
            }
        }

        stage('Dependency Check') {
            steps {
                dependencyCheck odcInstallation: 'Default',
                                stopBuild: false,
                                failBuildOnCVSS: '11' // Optional: Never fail unless CVSS > 10
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
