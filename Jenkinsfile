pipeline {
    agent any

    environment {
        DEBIAN_FRONTEND = 'noninteractive'
    }

    stages {
        stage('Install Apache2') {
            steps {
                echo 'Updating package list and installing Apache2...'
                sh '''
                    set -e
                    sudo apt-get update -qq
                    sudo apt-get install -y apache2
                '''
            }
        }

        stage('Start Apache2 Service') {
            steps {
                echo 'Starting Apache2 service...'
                sh '''
                    sudo systemctl start apache2
                    sudo systemctl enable apache2
                '''
            }
        }

        stage('Check Apache Logs for Errors') {
            steps {
                echo 'Checking Apache access logs for 4xx and 5xx HTTP errors...'
                sh '''
                    LOG_FILE="/var/log/apache2/access.log"
                    if [ -f "$LOG_FILE" ]; then
                        grep -E 'HTTP/1\\.[01]' "$LOG_FILE" | grep -E ' 4[0-9]{2} | 5[0-9]{2} ' || echo 'No 4xx or 5xx errors found'
                    else
                        echo "Log file $LOG_FILE not found."
                    fi
                '''
            }
        }
    }

    post {
        failure {
            echo 'Build failed! Please check the Apache logs and Jenkins console output.'
        }
        success {
            echo 'Pipeline completed successfully. Apache is installed and running.'
        }
    }
}


// pipeline {
//     agent any
//
//     stages {
//         stage('Install Apache2') {
//             steps {
//                 sh '''
//                 sudo apt-get update
//                 sudo apt-get install -y apache2
//                 '''
//             }
//         }
//
//         stage('Check Apache Logs') {
//             steps {
//                 sh '''
//                 sudo grep -E 'HTTP/1.[01]' /var/log/apache2/access.log | grep -E ' 4[0-9]{2} | 5[0-9]{2} ' || echo 'No 4xx or 5xx errors found'
//                 '''
//             }
//         }
//     }
// }
