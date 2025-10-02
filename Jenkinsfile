pipeline {
    agent any

    environment {
        DEV_SERVER_IP = '192.168.56.105'   // your server IP
        USERNAME = 'marium'                // your username
    }

    stages {

        stage('Show Deleted Files') {
            steps {
                echo "🔍 Checking for deleted files compared to previous commit..."

                // This command filters only deleted files (status D)
                sh '''
                    echo "Deleted files in the last commit:"
                    git diff --diff-filter=D --name-only HEAD~1 HEAD || echo "No files deleted"
                '''
            }
        }

        stage('Show All Changes') {
            steps {
                echo "📁 Full change summary between last two commits:"
                sh '''
                    git diff --name-status HEAD~1 HEAD
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploying to ${DEV_SERVER_IP}..."
                sh """
                    rsync -av --delete --itemize-changes --exclude ".git/" ${WORKSPACE}/* ${USERNAME}@${DEV_SERVER_IP}:/var/www/devoptest/
                """
            }
        }
    }
}
