pipeline {


    agent {
        label 'local'
    }


    stages {


        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/BuildBuddy50/testjenkins.git'
            }
        }


        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }


        stage('Install Browsers') {
            steps {
                bat 'npx playwright install'
            }
        }


        stage('Run Tests') {
            steps {
                bat 'npx playwright test'
            }
        }
    }


    post {
        always {
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'playwright-report',
                reportFiles: 'index.html',
                reportName: 'Playwright Report'
            ])
             archiveArtifacts artifacts: 'playwright-report/**', fingerprint: true
        }
    }
}
