pipeline {
    agent any

    stages {
        stage('Confirm GitHub checkout') {
            steps {
                echo 'Jenkins ne GitHub repository checkout ki.'
                sh 'git log -1 --oneline'
            }
        }
    }
}
