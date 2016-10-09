node('docker-j1.7mvn3') {
    stage('Checkout')
        checkout scm

    stage('Build')
        sh "mvn clean package -Dmaven.test.failure.ignore"

    stage('Test')
        parallel 'test': {
            sh "echo 'testing...'"
        }, 'verify': {
            sh "mvn verify -Dmaven.test.failure.ignore"
        }

    stage('archive')
        parallel 'jarResults': {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }, 'testResults': {
            junit '**/target/surefire-reports/TEST-*.xml'
        }
}

node {
    stage('Deploy')
        input 'All ok to deploy?'
        sh 'echo Deploying..'
}