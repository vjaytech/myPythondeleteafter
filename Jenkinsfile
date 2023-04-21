pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID='361703069140'
        AWS_DEFAULT_REGION='ap-southeast-1'
        IMAGE_REPO_NAME='maventestrepo'
        REPOSITORY_URI = '361703069140.dkr.ecr.ap-south-1.amazonaws.com/mavenwebapp'
        AWS_ACCESS_KEY_ID = "AKIAXEICFCS2GN56V566"
       AWS_SECRET_ACCESS_KEY = "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"
  }

    stages {
        stage('code fetch') {
            steps {
                git branch: 'main', url: 'https://github.com/vjtechie/mavenwebappsandbox.git'
            }
        }
        stage('Build packages') {
            steps {
                sh "mvn clean package"
            }
        }
         
         stage('Build docker image') {
            steps {
                
                sh "docker build -t mavenwebapp ."
            }
        }
        stage('push docker image') {
            steps {
                sh "aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 490167669940.dkr.ecr.ap-southeast-1.amazonaws.com"
                sh "docker tag maventestrepo:latest 490167669940.dkr.ecr.ap-southeast-1.amazonaws.com/maventestrepo:latest"
                sh "docker push 490167669940.dkr.ecr.ap-southeast-1.amazonaws.com/maventestrepo:latest"
            }
        }
        
    }
}
   
