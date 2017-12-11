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
                try {
                   timeout(time: 3, unit: 'MINUTES') {
                    input message:'Approve deployment?', submitter: 'hans'
                   }
                   mvn isntall
                }
                catch (err) { // timeout reached or input false
                   def user = err.getCauses()[0].getUser()
                   if('SYSTEM' == user.toString()) { // SYSTEM means timeout.
                       didTimeout = true
                   } else {
                       userInput = false
                       echo "Aborted by: [${user}]"
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
