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
                    if (isUnix()) {
                        def logContent = sh(script: 'sudo cat /var/log/apache2/error.log', returnStdout: true)
                        if (logContent.contains(" 4[0-9][0-9] ") || logContent.contains(" 5[0-9][0-9] ")) {
                            echo "Error(s) found in Apache logs!"
                            currentBuild.result = 'FAILURE'
                        } else {
                            echo "No errors found in Apache logs."
                        }
                    } else {
                        echo "Platform not supported"
                    }
                }
            }
        }
    }
}

