pipeline {
    agent any

    tools {
        maven 'maven-local'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/jaiswaladi246/Boardgame.git'
            }
        }
        stage('Testing') {
            steps {
                sh "mvn test"
            }
        }

        stage('Package') {
            steps {
                sh "mvn package"
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                     sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=BG -Dsonar.projectName=BG -Dsonar.java.binaries=target'''
                    }
            }
        }
    }
}
