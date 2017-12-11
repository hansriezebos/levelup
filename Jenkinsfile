pipeline {
    agent any
    
    tools {
maven 'M3'
jdk 'JDK8'
}


    stages {
        stage('Build') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn verify -Pintegrationtest'
            }
        }
        stage('Deploy') {
            steps {
                timeout(time: 3, unit: 'MINUTES') {
                    input message:'Approve deployment?', submitter: 'hans'
                    mvn install
                }
            }
        }
    }
    post {
        always {
            echo 'post'
            //junit '**/target/*.xml'
        }
        success {
            echo 'The Pipeline succeeded :)'
        }
        failure {
            echo 'The Pipeline failed :('
        }
    }
}
