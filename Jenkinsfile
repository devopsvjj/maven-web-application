node 
{
  def mavenHome = tool name: "maven3.8.1"
   
  stage('Checkoutcode')
  {
  git branch: 'development', credentialsId: '01e27f3f-c484-448f-9139-3136dc5b19ed', url: 'https://github.com/devopsvjj/maven-web-application.git'
  }
  stage('Buid')
  {
  sh "${mavenHome}/bin/mvn clean package"
  }
  stage('ExecuteSonarQubeReport')
  {
  sh "${mavenHome}/bin/mvn sonar:sonar"
  }
  stage('UploadArtifactintoNexus')
  {
  sh "${mavenHome}/bin/mvn deploy"
  }
  stage('DeployIntoTomcatServer')
  {
  sshagent(['b10c2b47-d5f7-4104-b671-f73590e3a7ae']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@99.79.74.69:/opt/apache-tomcat-9.0.46/webapps"
  }
  }
  stage('EmailNotification')
  {
  emailext body: '''regards
  Vijay''', subject: 'Build over...', to: 'sevakulavijaykumar@gmail.com'
  }
  
}
