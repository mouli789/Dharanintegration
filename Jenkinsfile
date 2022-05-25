pipeline {
    agent any

    stages {
        stage('git') {
            steps {
                git credentialsId: 'Dharanintegration' , url:  'https://github.com/mouli789/Dharanintegration.git' 
            }
        }
        
        stage('build') {
            steps {
                sh 'docker build -t myjenkinsrepo . '
            }
        }

        stage('aws') {
            steps {
                sh 'docker tag myjenkinsrepo:latest 569381932315.dkr.ecr.ap-south-1.amazonaws.com/myjenkinsrepo:latest'
            }
        }
        stage('aws login') {
            steps {
                sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 569381932315.dkr.ecr.ap-south-1.amazonaws.com'


            }
        }

        stage('aws push') {
            steps {
                sh 'docker push 569381932315.dkr.ecr.ap-south-1.amazonaws.com/myjenkinsrepo:latest'
            }
        }
