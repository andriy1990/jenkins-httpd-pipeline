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
