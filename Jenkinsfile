pipeline {
    agent any

    environment {
        APP_NAME = "calculator-app-java"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Gopikrishna398/calculator.git'
            }
        }

        stage('Clean Workspace') {
            steps {
                bat '''
                if exist build rmdir /s /q build
                if exist *.jar del /f /q *.jar
                if exist *.zip del /f /q *.zip
                '''
            }
        }

        stage('Compile Java') {
            steps {
                bat '''
                mkdir build
                javac -d build src\\Hello.java
                '''
            }
        }

        stage('Create JAR') {
            steps {
                bat '''
                jar cfe hello.jar Hello -C build .
                '''
            }
        }

        stage('Create ZIP Package') {
            steps {
                bat '''
                powershell Compress-Archive -Path hello.jar -DestinationPath %APP_NAME%-%BUILD_NUMBER%.zip
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: '*.zip', fingerprint: true
        }
    }
}
