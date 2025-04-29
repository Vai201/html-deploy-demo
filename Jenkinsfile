pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\xampp\\htdocs\\html-site'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Vai201/html-deploy-demo.git'
            }
        }

        stage('Clean Deployment Folder') {
            steps {
                bat """
                if exist "%DEPLOY_DIR%" (
                    rmdir /S /Q "%DEPLOY_DIR%"
                )
                mkdir "%DEPLOY_DIR%"
                """
            }
        }

        stage('Deploy HTML Files to XAMPP') {
            steps {
                bat """
                xcopy /E /Y /I "%WORKSPACE%\\*.html" "%DEPLOY_DIR%\\"
                """
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully.'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
