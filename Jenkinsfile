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
                // Add your actual build step (e.g., sh 'mvn clean install')
            }
        }

        stage('Dependency Check') {
            steps {
                // Run dependency check
                dependencyCheck odcInstallation: 'Default',
                                stopBuild: false

                // Move report to known directory if needed
                sh 'mkdir -p dependency-check-report && cp -r dependency-check-report.html dependency-check-report/index.html || true'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true

            // Publish HTML report
            publishHTML(target: [
                allowMissing: true,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'dependency-check-report',
                reportFiles: 'index.html',
                reportName: 'Dependency-Check Report'
            ])
        }
    }
}
