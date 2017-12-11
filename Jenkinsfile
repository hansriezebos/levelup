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
                timeout(time:5, unit:'DAYS') {
                    input message:'Approve deployment?'
                }
                retry(3) {
                    echo 'Deploying....'
                }

                timeout(time: 3, unit: 'MINUTES') {
                    echo "Done health check!"
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
