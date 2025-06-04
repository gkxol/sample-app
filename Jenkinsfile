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
                // Example: sh 'mvn clean install'
            }
        }

        stage('Dependency Check') {
            steps {
                dependencyCheck odcInstallation: 'Default', stopBuild: false

                // Prepare report for publishing
                sh '''
                    if [ -f dependency-check-report.html ]; then
                        mkdir -p dependency-check-report
                        mv dependency-check-report.html dependency-check-report/index.html
                    fi
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true

            // Publish HTML report (requires plugin)
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
