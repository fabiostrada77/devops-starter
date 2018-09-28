node {
    def mvnHome = tool "Maven"
    
    try {
    
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
	    
	    stage("Store artifact") {
	    	echo 'INIZIO STORE ARTIFACT'
	        archiveArtifacts artifacts: 'target/zip-service-jar-with-dependencies.jar', fingerprint: true
	        echo 'FINE STORE ARTIFACT'
	    }    
    } finally {
        junit 'target/surefire-reports/**/*.xml'
        junit 'target/failsafe-reports/**/*.xml'
        step([$class: 'JacocoPublisher'])
    }
}