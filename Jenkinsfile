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
                    // Виконуємо команду grep для пошуку строк з ' 4xx' або ' 5xx' в /var/log/apache2/error.log
                    def result = sh(script: "sudo grep ' 4xx' /var/log/apache2/error.log || sudo grep ' 5xx' /var/log/apache2/error.log", returnStatus: true)
                    
                    // Перевіряємо, чи була успішно виконана команда grep
                    if (result == 0) {
                        echo "No 4xx or 5xx errors found in error log."
                    } else {
                        echo "Error log contains 4xx or 5xx errors."
                        // Виводимо вміст error.log, якщо є помилки
                        sh "sudo cat /var/log/apache2/error.log"
                    }
                }
            }
        }
    }
}
