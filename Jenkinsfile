pipeline {
    agent any

    environment {
        // Optional: Add environment variables here
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
                // Add your actual build commands here
            }
        }

        stage('Dependency Check') {
            steps {
                dependencyCheck odcInstallation: 'Default', 
                                isAutoupdateDisabled: true, 
                                outdir: 'dependency-check-report',
                                scanpath: '.', 
                                suppressionFile: '', 
                                additionalArguments: ''
            }
        }
    }

    post {
        always {
            // No need to wrap this in `node {}` inside post
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
