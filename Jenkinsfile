pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
           }
        stage('upload war to Nexus'){
            steps{
                 nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: 'target/simple-app-1.0.0.war', type: 'war']], credentialsId: 'nexus3', groupId: 'in.javahome', nexusUrl: '18.232.120.232:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'http://18.232.120.232:8081/repository/maven-releases', version: '1.0.0'
            }
           }
        }
}