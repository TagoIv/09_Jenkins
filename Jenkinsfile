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
                 sh 'sudo grep -E '4[0-9]{2}|5[0-9]{2}' /var/log/apache2/error.log' 
            }
        }
    }
}
