pipeline {
    agent any
    stages {
        stage("Restore project dependencies") {
            when {
                branch 'main'    // <-- only run this stage on main branch
            }
            steps {
                bat 'dotnet restore'
            }
        }
        stage("Build the project") {
            when {
                branch 'main'    
            }
            steps {
                bat 'dotnet build --no-restore'
            }
        }
        stage ("Run tests") {
            when {
                branch 'main'    
            }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}