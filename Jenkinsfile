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
                input message:'Approve deployment?', submitter: 'hans'
                timeout(time: 3, unit: 'MINUTES') {
                    retry(3) {
                        sh 'mvn test'
                    }
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
