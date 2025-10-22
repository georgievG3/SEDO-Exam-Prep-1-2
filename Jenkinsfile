pipeline {
    agent any

    environment {
        DOTNET_CLI_TELEMETRY_OPTOUT = '1'
        DOTNET_SKIP_FIRST_TIME_EXPERIENCE = '1'
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
                bat 'dotnet test --no-build --configuration Release --verbosity normal --logger "trx;LogFileName=test_results.trx"'
            }
        }
    }

    post {
        always {
            junit '**/TestResults/*.trx'

            echo 'Pipeline finished.'
        }
    }
}
