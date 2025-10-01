pipeline {
    agent any

    environment {
        DEV_SERVER_IP = '192.168.56.105'  // Replace with your actual IP address
        USERNAME = 'marium'               // Replace with your actual username
        PRIVATE_KEY_PATH = '/var/lib/jenkins/.ssh/id_ed25519'
    }

    stages {

        stage('Show Changes') {
            steps {
                echo "🔍 Checking what changed in the last commit..."
                sh '''
                    echo "Changes between the last two commits:"
                    git diff --name-status HEAD~1 HEAD || echo "No previous commit to compare."
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploying to ${DEV_SERVER_IP}..."

                // ✅ Add --delete + --itemize-changes here
                sh """
                    rsync -av --delete --itemize-changes --exclude ".git/" ${WORKSPACE}/* ${USERNAME}@${DEV_SERVER_IP}:/var/www/devoptest/
                """
            }
        }
    }
}
