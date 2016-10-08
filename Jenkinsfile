node('docker-1.7mvn3') {
    stage 'Checkout'
    checkout scm

    stage 'Build'
    sh "mvn clean package"

    stage 'Test'
    parallel 'test': {
        sh "echo 'testing...'"
    }, 'verify': {
        sh "echo 'verifying...'"
    }

    stage 'archive'
    archive 'target/*.jar'
}


node {
    stage 'Deploy'
    sh 'echo Deploying..'
}