pipeline {
  agent {
    docker { image 'maven:3.8.1-adoptopenjdk-11' }
  }
  stages{
    stage('Deploy'){
      steps{
        git credentialsId: 'git-token', url: 'https://github.com/odeshman/maven-web-app.git'
      }
    }
    stage('Maven Build'){
      steps{
        sh 'mvn clean package'
      }
    }
    stage('Deploy'){
      steps{
        sshagent(['tomcat-agent']){
            sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/project-pipeline/target/maven-web-app.war ubuntu@34.235.111.139:/opt/tomcat/webapps'
        }
      }
    }
  }
 }

