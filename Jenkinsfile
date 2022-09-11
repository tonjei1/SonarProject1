pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/etechDevops/etech-mavenApp.git']]])
      }
    }
    stage('2-cleanws'){
      steps{
        sh 'mvn clean'
      }
    }
    stage('3-mavenbuild'){
      steps{
        sh 'mvn package'
      }
    }
    stage('unittest'){
      steps{
          sh 'mvn test'
      }
    }
    stage('codequality'){
      steps{
        sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=tonjei_pro \
  -Dsonar.host.url=http://ec2-3-141-188-125.us-east-2.compute.amazonaws.com:9000 \
  -Dsonar.login=sqp_ddbd740884514fcabb7e11801d48cbf2ab517bf3'
      }
    }
  }
}