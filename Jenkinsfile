node {
    stage 'Checkout'
    checkout scm

    def mvnHome = tool "mvn3"

    stage 'Build'
    sh "${mvnHome}/bin/mvn clean package"

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
    sh 'echo "Not yet written!"'
}