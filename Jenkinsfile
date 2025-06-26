pipeline {
    agent any

    stages {
        stage('Install Apache2') {
            steps {
                sh '''
                sudo apt-get update
                sudo apt-get install -y apache2
                '''
            }
        }

        stage('Check Apache Logs') {
            steps {
                sh '''
                sudo grep -E 'HTTP/1.[01]' /var/log/apache2/access.log | grep -E ' 4[0-9]{2} | 5[0-9]{2} ' || echo 'No 4xx or 5xx errors found'
                '''
            }
        }
    }
}


// pipeline {
//     agent any
//     stages {
//         stage('Install Apache2') {
//             steps {
//                 sh '''
//                     # Update package list
//                     sudo apt-get update -y
//
//                     # Install Apache2
//                     sudo apt-get install -y apache2
//
//                     # Start Apache2 service
//                     sudo systemctl start apache2
//
//                     # Enable Apache2 to run on boot
//                     sudo systemctl enable apache2
//
//                     # Verify Apache2 is running
//                     if systemctl is-active --quiet apache2; then
//                         echo "Apache2 is successfully installed and running"
//                     else
//                         echo "Apache2 installation failed or service is not running"
//                         exit 1
//                     fi
//                 '''
//             }
//         }
//     }
//     post {
//         success {
//             echo 'Apache2 installation completed successfully'
//         }
//         failure {
//             echo 'Apache2 installation failed'
//         }
//     }
// }


// pipeline {
//     agent any
//
//     environment {
//         REMOTE_HOST = "127.0.0.1"
//         REMOTE_PORT = "2222"
//         SSH_KEY_ID = "vagrant-key" // ID із Jenkins Credentials
//         REMOTE_USER = "vagrant"
//         SSH_OPTS = "-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null"
//     }
//
//     stages {
//         stage('Install Apache2') {
//             steps {
//                 sshagent (credentials: [env.SSH_KEY_ID]) {
//                     sh """
//                     ssh ${env.SSH_OPTS} -p ${env.REMOTE_PORT} ${env.REMOTE_USER}@${env.REMOTE_HOST} \\
//                     'sudo apt-get update && sudo apt-get install -y apache2'
//                     """
//                 }
//             }
//         }
//     }
// }
//
//         stage('Check Apache Logs') {
//             steps {
//                 sshagent (credentials: [env.SSH_KEY_ID]) {
//                     sh """
//                     ssh -o StrictHostKeyChecking=no -p ${env.REMOTE_PORT} ${env.REMOTE_USER}@${env.REMOTE_HOST} \\
//                     "sudo grep -E 'HTTP/1.[01]' /var/log/apache2/access.log | grep -E ' 4[0-9]{2} | 5[0-9]{2} ' || echo 'No 4xx or 5xx errors found'"
//                     """
//                 }
//             }
//         }
//     }
// }
