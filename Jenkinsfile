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
            //junit '**/target/*.xml'
        }
        succeeded {
            echo 'The Pipeline succeeded :)'
        }
        failure {
            echo 'The Pipeline failed :('
        }
    }
}
