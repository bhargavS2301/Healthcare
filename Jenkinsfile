pipeline {
    agent any
    tools {
        maven 'maven'
    }
 
    stages {
        stage('Git-Code-Checkout') {
            steps {
                git 'https://github.com/bhargavS2301/Healthcare.git'
            }
        }
      
        stage('Code Build') {
            steps {
                sh 'mvn clean install'
            }
        } 
       }
    
    }

