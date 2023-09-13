pipeline {
    agent any
    tools {
        Maven 'maven'
    }
 
    stages {
        stage('Git-Code-Checkout') {
            steps {
                git 'https://github.com/bhargavS2301/Healthcare.git'
            }
        }
       stages {
        stage('Code Build') {
            steps {
                sh 'mvn clean install'
            }
        } 
       }
    }
    }

