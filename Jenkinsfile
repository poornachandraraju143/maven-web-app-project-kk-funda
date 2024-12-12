node
{

def mavenHome = tool name: "maven-3.9.9"
	stage('checkout')
  {
    git branch: 'development', credentialsId: 'e886ebbe-aa31-463e-b5f0-446c712f9f17', url: 'https://github.com/poornachandraraju143/maven-web-app-project-kk-funda.git'

	}
	  stage('create package')
	{
	  sh "${mavenHome}/bin/mvn clean package"
	}
	  stage('SQ report')
	{
	  sh "${mavenHome}/bin/mvn clean package sonar:sonar"
	}
	  stage('upload artfactory')
	{
	  sh "${mavenHome}/bin/mvn clean package sonar:sonar deploy"
	}
	 stage('deploytotomcat')
	{
	 sshagent(['f405c620-03e2-417b-b95f-0f904608f521']) {
     // some block
 
      sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.203.74.138:/opt/apache-tomcat-9.0.97/webapps"
	}
  }

}
