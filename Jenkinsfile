pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    options {
  buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
           }
        stage('upload war to Nexus'){
            steps{
                script {
                 def mavenPom = readMavenPom file: 'pom.xml'
                 def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "simpleapp-snapshot" : "simpleapp-release"
                 nexusArtifactUploader artifacts: [
                     [artifactId: 'simple-app', 
                     classifier: '', 
                     file: "target/simple-app-${mavenPom.version}.war", 
                     type: 'war']], 
                     credentialsId: 'nexus3', 
                     groupId: 'in.javahome', 
                     nexusUrl: '18.232.120.232:8081', 
                     nexusVersion: 'nexus3',
                     protocol: 'http', 
                     repository: nexusRepoName, 
                     version: "${mavenPom.version}"
                }
                 
            }
           }
        }
}