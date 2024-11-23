pipeline {
  agent any
  tools { 
        maven 'Maven_3_2_5'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {  
        sh '''mvn clean verify sonar:sonar 
              -Dsonar.projectKey=sample125_sam
              -Dsonar.organization=sample125" 
              -Dsonar.host.url=https://sonarcloud.io 
              -Dsonar.token=485d7640bbf69797c36fdf0d1983b6b1ac596c5d'''
      }
        } 

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
