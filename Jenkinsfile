pipeline {
    agent any
    tools {
        maven 'maven'
    }
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
    }
     parameters {
        booleanParam(name: 'skip_test', defaultValue: false, description: 'Set to true to skip the test stage')
    }
 
    stages {
        stage('Git-Code-Checkout') {
            steps {
                git 'https://github.com/bhargavS2301/Healthcare.git'
            }
        }
      
        stage('Code compile') {
            when { expression { params.skip_test != false } }
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
        stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
          stage('Code Build') {
            steps {
                sh 'mvn clean install'
            }
        } 
        stage('Artifact Upload-Deploy') {
          steps {
           nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: '15.207.247.180:8081',
        groupId: 'com.project.staragile',
        version: '0.0.1-SNAPSHOT',
        repository: 'Healthcare',
        credentialsId: 'nexus-cred',
        artifacts: [
            [artifactId: 'medicure',
             classifier: '',
             file: 'target/medicure-0.0.1-SNAPSHOT.jar',
             type: 'jar']
        ]
     )
      }
    }
            
       }
    }
    
    

