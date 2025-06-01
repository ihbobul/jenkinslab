pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ihbobul/jenkinslab', credentialsId: 'jenkins-lab-pass'
            }
        }
        
        stage('Build') {
            steps {
                // Corrected the quoting for the MSBuild path
                bat '"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" test_repos.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Use the correct configuration output folder (Release vs Debug)
                bat "x64\\Release\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

    post {
        always {
            // Publish test results using the junit step
            junit 'test_report.xml'
        }
    }
}
