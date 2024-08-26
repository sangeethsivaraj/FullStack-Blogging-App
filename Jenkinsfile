pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sangeethsivaraj/FullStack-Blogging-App.git'
            }
        }
        stage('maven compile'){
            steps {
                sh 'mvn compile'
            }
        }
        stage('maven test'){
            steps {
                sh 'mvn test'
            }
        }
        stage('sonar scanner'){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=nexus-practice \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=nexus-practice '''
                }
            }
        }
        stage('build and push to nexus'){
            steps{
                withMaven(globalMavenSettingsConfig: '', jdk: '', maven: 'maven3', mavenSettingsConfig: '434cee7f-3027-464a-adc7-587f9c950d4e', traceability: true) {
                    sh'mvn deploy'
                }
            }
        }
        
    }
}
