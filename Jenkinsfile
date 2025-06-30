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
                sshPublisher(publishers: [sshPublisherDesc(configName: 'TomcatServer', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/usr/share/tomcat/webapps', remoteDirectorySDF: false, removePrefix: 'webapp/target/', sourceFiles: 'webapp/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])       
            }
        }
    }   
}
