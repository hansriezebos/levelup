pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
    post {
        always {
            junit '**/target/*.xml'
        }
        success {
            echo 'The Pipeline succeeded :)'
        }
        failure {
            echo 'The Pipeline failed :('
        }
    }
}
