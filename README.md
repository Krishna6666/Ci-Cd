# Ci-Cd
Script for declerative pipeline
{
    agent any
    stages
    {
     stage('cont dwnld')
     {
      steps
      {
      git 'https://github.com/intelliqittrainings/maven.git'
      }
     }
     stage('cont bld')
     {
      steps
      {
      sh label:'' , script: 'mvn package'
      }
     }
     stage('cont dplymnt')
     {
      steps
      {
      sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/CI-CD/webapp/target/webapp.war ubuntu@172.31.4.161:/var/lib/tomcat8/webapps/test.war'
      }
     }
     stage('cont tstng')
     {
      steps
      {
      git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
      sh label: '', script: 'java -jar testing.jar'
      }
     }
     stage('cont dlvry')
      {
      steps
      {
      sh label: '', script: 'scp /home/ubuntu/.jenkins/workspace/CI-CD/webapp/target/webapp.war ubuntu@172.31.1.35:/var/lib/tomcat8/webapps/prod.war'
      }
     }
    }
}
