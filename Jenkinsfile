node('Exacnode'){ 
   def scannerHome = tool 'SonarQubeScanner'
   stage('Preparation') {

	git url: 'https://github.com/LearnShareKnowledge/demo_1.git', branch: 'master' 
   }
   
   stage('Build') {
   	sh 'chmod 755 LearnShareKnowledgeDemoProject/gradlew;cd LearnShareKnowledgeDemoProject/;./gradlew clean build'       
   }
   stage('Signing project'){
        signAndroidApks (
        	keyStoreId: "debug.keystore",
        	keyAlias: "android",
        	apksToSign: "**/*app-release-unsigned.apk"
	)
	
   }
   
   stage('Send code to Sonar') {
      sh "${scannerHome}/bin/sonar-scanner -Dsonar.login=sonar -Dsonar.password=sonar -Dsonar.sources=. -Dsonar.projectVersion=1.0 -Dsonar.projectKey=my_project -Dsonar.projectName=my_project -Dsonar.jdbc.username=sonar -Dsonar.jdbc.password=sonar" 
   }

}
