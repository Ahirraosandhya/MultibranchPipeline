pipeline {
    agent any
    tools {
        maven 'MAVEN'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'cb5c227d-1619-4aa0-9c92-7e7cce0c495c', url: 'https://github.com/Ahirraosandhya/Jenkins_CICD.git']])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    sh 'docker build -t sandhyadockerac/my-app-1.0 .'
                }
            }
        }
        stage('Deploy Docker Image'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'sandhyadockerac', variable: 'dockerhubpwd')]) {
                     sh 'docker login -u sandhyadockerac -p ${dockerhubpwd}'
                 }  
                 sh 'docker push sandhyadockerac/my-app-1.0'
                }
            }
        }
   }
                    
}

