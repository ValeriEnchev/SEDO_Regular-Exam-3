pipeline {
    agent any

    triggers {
        // Automatically build when changes are pushed to 'main'
        pollSCM('H/5 * * * *') // Poll every 5 minutes (use webhook if available)
    }

    stages {
        stage('Check branch') {
            steps {
                script {
                    if (env.BRANCH_NAME != 'main') {
                        echo "Skipping build for branch: ${env.BRANCH_NAME}"
                        currentBuild.result = 'SUCCESS'
                        return
                    }
                }
            }
        }
        stage("Restore project dependencies") {

            steps {
                bat 'dotnet restore'
            }
        }
        stage("Build the project") {

            steps {
                bat 'dotnet build --no-restore'
            }
        }
        stage ("Run tests") {

            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}