pipeline {
    agent any
    tools {
        maven 'maven'
    }
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "15.207.247.180:8081"
        NEXUS_REPOSITORY = "Healthcare"
        NEXUS_CREDENTIAL_ID = "nexus-cred"
    }
 
    stages {
        stage('Git-Code-Checkout') {
            steps {
                git 'https://github.com/bhargavS2301/Healthcare.git'
            }
        }
      
        stage('Code compile') {
            steps {
                sh 'mvn clean compile'
            }
        } 
         stage ('Sonar-Analysis') {
             steps {
                 withSonarQubeEnv('sonar-scanner') {
                     sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Healthcare \
                     -Dsonar.java.binaries=. \
                     -Dsonar.projectKey=Healthcare '''
                 }
             }
         }
          stage('Code Build') {
            steps {
                sh 'mvn clean install'
            }
        } 
         stage  ('artifact upload') {
             steps {
                 sh ''' nexusArtifactUploader credentialsId: 'nexus-cred', 
                        groupId: 'org.springframework.boot', 
                        nexusUrl: '15.207.247.180:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', repository: 'http://15.207.247.180:8081/repository/Healthcare/', 
                        version: '2.7.4 '''
             
         }
        
        
       }
    }
    
    }
    }

