pipeline {
    agent any

    stages {
        stage('Checkout code') {
            steps {
                // Checkout code from GitHub and specify the branch
                git branch: 'main', url: 'https://github.com/Ronito88/JenkinsSeleniumBasicExercise'
            }
        }
          stage('Set up .NET Core') {
            steps {
                bat '''
                echo Installing .NET SDK 6.0
                curl -l -o dotnet-sdk-6.0.132-win-x64.exe https://download.visualstudio.microsoft.com/download/pr/0c82e7e6-fdde-49f2-a69f-bd986aeafe1b/9ea7411a22e661fff0e61e56a466e484/dotnet-sdk-6.0.132-win-x64.exe
                echo installing dotnet-sdk-6.0.132-win-x64.exe   
                dotnet-sdk-6.0.132-win-x64.exe /quiet /norestart
                    '''
            }
        }
         stage('Restore dependencies') {
            steps {
                // Restore dependencies using the solution file
                bat 'dotnet restore SeleniumBasicExercise.sln'
            }
        }

        stage('Build') {
            steps {
                // Build the project using the solution file
                bat 'dotnet build SeleniumBasicExercise.sln --configuration Release'
            }
        }
         stage('Run tests TestProject1') {
            steps {
                // Run tests using the solution file
                bat 'dotnet test TestProject1/TestProject1.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
         stage('Run tests TestProject2') {
            steps {
                // Run tests using the solution file
                bat 'dotnet test TestProject2/TestProject2.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
         stage('Run tests TestProject3') {
            steps {
                // Run tests using the solution file
                bat 'dotnet test TestProject3/TestProject3.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
    }

     post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step([
            $class: 'MSTestPublisher',
            testResultsFile:'**/TestResults/*.trx'
           ])
        }
    }
}
