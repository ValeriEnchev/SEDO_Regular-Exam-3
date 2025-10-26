pipeline {
    agent any
    stages {
        stage("Restore project dependencies") {
            when {
                branch pattern: "(main)", comparator: "REGEXP"
            }
            steps {
                bat 'dotnet restore'
            }
        }
        stage("Build the project") {
            when {
                branch pattern: "(main)", comparator: "REGEXP"    
            }
            steps {
                bat 'dotnet build --no-restore'
            }
        }
        stage ("Run tests") {
            when {
                branch pattern: "(main)", comparator: "REGEXP"   
            }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}