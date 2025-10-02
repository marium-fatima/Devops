pipeline {
    agent any

    environment {
        DEV_SERVER_IP = '192.168.56.105'   // your server IP
        USERNAME = 'marium'                // your username
    }

    stages {

        stage('Deploy') {
            steps {
                echo "🚀 Deploying to ${DEV_SERVER_IP}..."
                sh """
                    rsync -av --delete --exclude ".git/" ${WORKSPACE}/* ${USERNAME}@${DEV_SERVER_IP}:/var/www/devoptest/
                """
            }
        }
    }
}
