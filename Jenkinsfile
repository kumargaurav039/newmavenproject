pipeline {
  agent any
  stages {
    stage('scm checkout') {
      steps {
        git 'https://github.com/kumargaurav039/newmavenproject.git'
      }
    }

    stage('package the code') {
      steps {

        withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
        sh 'mvn clean package'
        }
        
      }
    }

    stage('deploy the code on tomcat') {
      steps {

       sshagent(['DEVCICD']) {
        sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.8.251:/usr/share/tomcat/webapps'
        }
        
      }
    }

  }
}
