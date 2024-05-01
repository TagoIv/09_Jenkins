pipeline {
    agent any

    stages {
        stage('Install Apache2') {
            steps {
                sh 'sudo apt-get update && sudo apt-get install -y apache2'
            }
        }
        stage('Read Apache Logs') {
            steps {
                script {
                    // SSH to remote VM and read Apache logs
                    def logContent = sshCommand remote: 'your_remote_vm_ip', user: 'your_remote_vm_user', password: 'your_remote_vm_password', command: '''
                        cat /var/log/apache2/error.log
                    '''
                    
                    // Check for 4xx and 5xx errors
                    if (logContent.contains(" 4[0-9][0-9] ") || logContent.contains(" 5[0-9][0-9] ")) {
                        echo "Error(s) found in Apache logs!"
                        currentBuild.result = 'FAILURE'
                    } else {
                        echo "No errors found in Apache logs."
                    }
                }
            }
        }
    }
}

