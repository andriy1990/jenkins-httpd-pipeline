pipeline {
    agent any

    environment {
        LOG_PATH = "/var/log/apache2/access.log"
    }

    stages {
        stage('Update System & Install Apache2') {
            steps {
                echo 'Updating system and installing Apache2...'
                sh '''
                if command -v apt-get &> /dev/null; then
                    sudo apt-get update -y
                    sudo apt-get install -y apache2
                    sudo systemctl start apache2
                    sudo systemctl enable apache2
                elif command -v yum &> /dev/null; then
                    sudo yum install -y httpd
                    sudo systemctl start httpd
                    sudo systemctl enable httpd
                    export LOG_PATH="/var/log/httpd/access_log"
                else
                    echo "Unsupported OS"
                    exit 1
                fi
                '''
            }
        }

        stage('Check Apache Logs for Errors') {
            steps {
                echo 'Scanning Apache logs for 4xx and 5xx errors...'
                sh '''
                if [ -f "$LOG_PATH" ]; then
                    echo "Log file found at $LOG_PATH"
                    sudo grep -E 'HTTP/1.[01]' $LOG_PATH | grep -E ' [45][0-9]{2} ' || echo 'No 4xx or 5xx errors found.'
                else
                    echo "Log file not found: $LOG_PATH"
                    exit 1
                fi
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
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
