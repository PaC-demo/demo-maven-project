node('docker-j1.7mvn3') {

    stage('Checkout') {
        checkout scm
    }

    stage('Build') {
        sh "mvn clean package -DskipTests"
    }

    stage('Test') {
        parallel 'test': {
            sh "echo 'testing...'"
        }, 'verify': {
            sh "echo 'verifying...'"
        }
    }

    stage('archive'){
        parallel 'jarResults': {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }, 'testResults': {
            junit '**/target/surefire-reports/TEST-*.xml'
        }
    }

}

node {

    stage('Deploy') {
        //input 'All ok to deploy?'
        sh 'echo Deploying..'
    }

}