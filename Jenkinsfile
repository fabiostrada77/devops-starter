node {
    def mvnHome = tool "Maven"
    
    stage('checkout project') {
        echo 'INIZIO CHECKOUT PROJECT'
        checkout scm
        echo 'FINE CHECKOUT PROJECT'
    }
    
    stage('unit test'){
        echo 'INIZIO JUNIT TEST'
        sh "${mvnHome}/bin/mvn clean test" 
        echo 'FINE JUNIT TEST'
    }
    
    stage('integration test'){
        echo 'INIZIO INTEGRATION TEST'
        sh "${mvnHome}/bin/mvn test-compile failsafe:integration-test" 
        echo 'FINE INTEGRATION TEST'
    }
    
    stage('build'){
        echo 'INIZIO BUILD'
        sh "${mvnHome}/bin/mvn package" 
        echo 'FINE BUILD'
    }    
}