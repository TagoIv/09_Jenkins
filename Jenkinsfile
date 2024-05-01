pipeline {
    agent any

    stages {
        stage('Install Apache2') {
            steps {
                sh 'sudo apt-get update && sudo apt-get install -y apache2'
            }
        }
        stage('Check Logs for Errors') {
            steps {
                script {
                    def errorLog = sh(script: 'sudo grep -E " 4[0-9]{2}| 5[0-9]{2}" /var/log/apache2/error.log', returnStdout: true).trim()
                    
                    if (errorLog) {
                        echo "Error log contains 4xx or 5xx errors:"
                        echo errorLog
                    } else {
                        echo "No 4xx or 5xx errors found in error log."
                    }
                }
            }
        }
    }
}
