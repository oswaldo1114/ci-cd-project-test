pipeline {
    agent any
    tools {
        maven 'apache-maven-3.8.2'
        jdk 'jdk-8-221'
    }
    stages {
        stage('Test') { 
            steps {
                sh 'mvn clean test'
            }
        }
        stage('Clean') { 
            steps {
                sh 'mvn package -DskipTests'
            }
        }
        stage('Deploy') {
            when { anyOf { branch 'dev'; branch 'qa'; branch 'prod' } }
            steps {
                sh "mvn deploy -Denvironment=${GIT_BRANCH} -DmuleDeploy"
            }
        }
        
    }
}
