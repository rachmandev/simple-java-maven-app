// Scripted Jenkinsfile Created By Rachmandev
node {
    checkout scm
    docker.image('maven:3.9.0-eclipse-temurin-11').inside('-v /root/.m2:/root/.m2') {
        skipStagesAfterUnstable()
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }

        stage('Test') {
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }

        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy ?'
        }

        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            sleep time: 1, unit: 'MINUTES'
        }
    }
} 