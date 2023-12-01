pipeline {
  agent {
    docker { image 'maven:3.8.1-adoptopenjdk-11' }
  }
  stages{
    stage('Clone'){
      steps{
        git credentialsId: 'git-token', url: 'https://github.com/odeshman/maven-web-app.git'
      }
    }
    stage('Maven Build'){
      steps{
        sh 'mvn clean package'
      }
    }
    stage('Sleep'){
      steps{
            sh 'sleep 3600'
        }
      }
    }
    stage('Deploy'){
      steps{
        sshagent(['tomcat-agent']){
            sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/docker-pipeline/target/maven-web-app.war ubuntu@34.235.111.139:/opt/tomcat/webapps'
        }
      }
    }
  }
 }

