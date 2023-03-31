pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=pramods-devsecops-inc -Dsonar.organization=pramods-devsecops-inc  -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=37b04933c32aa2e4801ee2a211e25a896d932b6c'
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
