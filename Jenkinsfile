pipeline {
    agent any
    tools {
        maven 'maven'
    }
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
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
        
       }
    
    }

