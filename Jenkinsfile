pipeline {
    agent any
    stages{
        stage('scm checkout'){
            steps{
                git 'https://github.com/HarshalBhandare99/maven-project.git'
            }
        } 
        stage('mvn validate'){
            steps{
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                sh 'mvn validate'
                }
            }
        }
        stage('mvn compile'){
            steps{
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                sh 'mvn compile'
                }
            }
        }
        stage('mvn package'){
            steps{
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                sh 'mvn package'
                }
            }
        }
        stage('Deploy the package'){
            steps{
                sshagent(['Tomcat_Server']) {
                sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@52.66.200.20:/usr/share/tomcat/webapps'
                }       
            }
        }
    
    }   
}
