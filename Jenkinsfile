pipeline {
    agent any

    environment {
        REMOTE_HOST = "127.0.0.1"
        REMOTE_PORT = "2222"
        SSH_KEY_ID = "vagrant-key" //
        REMOTE_USER = "vagrant"
    }

    stages {
        stage('Install Apache2') {
            steps {
                sshagent (credentials: [env.SSH_KEY_ID]) {
                    sh """
                    ssh -o StrictHostKeyChecking=no -p ${env.REMOTE_PORT} ${env.REMOTE_USER}@${env.REMOTE_HOST} \\
                    'sudo apt-get update && sudo apt-get install -y apache2'
                    """
                }
            }
        }

        stage('Check Apache Logs') {
            steps {
                sshagent (credentials: [env.SSH_KEY_ID]) {
                    sh """
                    ssh -o StrictHostKeyChecking=no -p ${env.REMOTE_PORT} ${env.REMOTE_USER}@${env.REMOTE_HOST} \\
                    "sudo grep -E 'HTTP/1.[01]' /var/log/apache2/access.log | grep -E ' 4[0-9]{2} | 5[0-9]{2} ' || echo 'No 4xx or 5xx errors found'"
                    """
                }
            }
        }
    }
}
