node {
    stage 'Checkout'
    checkout scm

    def mvnHome = Tool "mvn3"

    stage 'Build'
    sh "${mvnHome}/bin/mvn clean package"

    stage 'Test'
    parallel 'test': {
        sh "${mvnHome}/bin/mvn test"
    }, 'verify': {
        sh "${mvnHome}/bin/mvn verify"
    }

    stage 'archive'
    archive 'target/*.jar'
}


node {
    stage 'Deploy'
    sh 'Not yet written!'
}