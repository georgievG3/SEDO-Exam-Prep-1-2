pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup .NET') {
            steps {
                bat 'dotnet --version'
            }
        }

        stage('Restore dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --no-restore --configuration Release'
            }
        }

        stage('Test') {
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }

    post {
        always {
            junit '**/TestResults/*.xml'
        }
        success {
            echo '✅ Build and tests succeeded!'
        }
        failure {
            echo '❌ Build or tests failed!'
        }
    }
}
