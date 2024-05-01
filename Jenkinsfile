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
                    def command = "sudo grep -E ' 4[0-9]{2}| 5[0-9]{2}' /var/log/apache2/error.log"
                    def result = sh(script: command, returnStatus: true)

                    if (result == 0) {
                        echo "No 4xx or 5xx errors found in error log."
                    } else {
                        echo "Error log contains 4xx or 5xx errors."
                        // Display the error log
                        sh "sudo grep -E ' 4[0-9]{2}| 5[0-9]{2}' /var/log/apache2/error.log"
                    }
                }
            }
        }
    }
}
