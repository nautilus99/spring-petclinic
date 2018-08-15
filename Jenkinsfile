pipeline {
    agent { label 'linux01' }
    stages {
        stage ('Checkout') {
          agent { docker 'maven:3.5-alpine' }
          steps {
            git 'https://github.com/nautilus99/spring-petclinic.git'
          }
        }
        stage('Build') {
            agent { docker 'maven:3.5-alpine' }
            steps {
                sh 'mvn clean package'
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage('Deploy') {
          steps {
            input 'Do you approve the deployment?'
            echo "deploying..."

            // copy the application
            // sh 'scp target/*.jar jenkins@192.168.50.10:/opt/pet/'
            // start the application
            // sh "ssh jenkins@192.168.50.10 'nohup java -jar /opt/pet/spring-petclinic-1.5.1.jar &'"
          }
        }
    }
}
