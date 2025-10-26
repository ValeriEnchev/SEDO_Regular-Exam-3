pipeline {
    agent any

    triggers {
        // Automatically build when changes are pushed to 'main'
        pollSCM('H/5 * * * *') // Poll every 5 minutes (use webhook if available)
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ValeriEnchev/SEDO_Regular-Exam-3.git'
            }
        }

        stage('Restore') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --configuration Release --no-restore'
            }
        }

        stage('Test') {
            steps {
                bat 'dotnet test --configuration Release --no-build --verbosity normal'
            }
        }
    }

    post {
        always {
            junit '**/TestResults/*.xml'
        }
        failure {
            echo '❌ Build or tests failed!'
        }
        success {
            echo '✅ Build and tests succeeded!'
        }
    }
}