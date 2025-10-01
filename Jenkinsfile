pipeline {
    agent any

    environment {
        DEV_SERVER_IP = '192.168.56.105'  // Replace with your actual IP address
        USERNAME = 'marium'               // Replace with your actual username
        PRIVATE_KEY_PATH = '/var/lib/jenkins/.ssh/id_ed25519'  // Path to the private key
    }

    stages {

        stage('Show Changes') {
            steps {
                echo "🔍 Checking what changed in the last commit..."
                // Show added (A), modified (M), and deleted (D) files
                sh '''
                    echo "Changes between the last two commits:"
                    git diff --name-status HEAD~1 HEAD || true
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploying to ${DEV_SERVER_IP}..."

                // Rsync deployment command with --delete to remove deleted files
                sh """
                    rsync -av --delete --exclude ".git/" ${WORKSPACE}/* ${USERNAME}@${DEV_SERVER_IP}:/var/www/devoptest/
                """
            }
        }
    }
}
