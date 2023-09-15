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
       
          stage('Code Build') {
            steps {
                sh 'mvn clean install'
            }
        } 
         stage('Docker Build') {
            steps {
                sh 'docker build -t bhargavk0702/javaapp .'
                }
        } 
        stage('Dcker image push') {
          steps {
              withCredentials([string(credentialsId: 'docker-cred', variable: 'docker')]) {
              sh 'docker login -u bhargavk0702 -p ${docker}'
              sh 'docker push bhargavk0702/javaapp:1.0'
}
          }
        }
       }
    }
    
    

