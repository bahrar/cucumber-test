pipeline {
  
agent any

  parameters {
		string (
			name: "PLAY",
			defaultValue:  "main.yml",
			description: "playbook à exécuter"
		)
		choice(name: 'ENV', choices: 'STAGE\nPROD', description: 'env où déployer')
  }
  
  tools {
    // jdk "jdk8"
	maven "M3"
  }
  
  environment {
    ENV = "PIC"
	VERSION = "1.0.1"
  }
 
stages{  
	stage ('Checkout'){
		steps {
        checkout scm
		}
	}
	
	stage ('Build') {
		steps {
			echo "building ${VERSION} ${ENV}"	
			// Run the maven build and upload artifacts to nexus repository
			echo "sh mvn test"
			sh "mvn test"
			step([$class: 'CucumberReportPublisher', fileExcludePattern: '', fileIncludePattern: '', ignoreFailedTests: false, jenkinsBasePath: '', jsonReportDirectory: '', missingFails: false, parallelTesting: false, pendingFails: false, skippedFails: false, undefinedFails: false])
		}
		
		
	}
	
	stage ('cleanup'){	
	  steps {
		  // Let's wipe out the workspace before we finish!
		  deleteDir()
		}
	  }	
 }
}

