pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID='xxxxxxxx'
        AWS_DEFAULT_REGION='ap-southeast-1'
        IMAGE_REPO_NAME='maventestrepo'
        REPOSITORY_URI = 'xxxxxxxxxxx.dkr.ecr.ap-south-1.amazonaws.com/mavenwebapp'
        AWS_ACCESS_KEY_ID = "xxxxxxxxxx"
       AWS_SECRET_ACCESS_KEY = "xxxxxxxxxxxxxx"
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
         
         stage('Build  image and push to ECR') {
            steps {
                sh "aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 490167669940.dkr.ecr.ap-southeast-1.amazonaws.com"
                sh "docker build -t maventestrepo ."
                sh "docker tag maventestrepo:latest 490167669940.dkr.ecr.ap-southeast-1.amazonaws.com/maventestrepo:latest"
                sh "docker push 490167669940.dkr.ecr.ap-southeast-1.amazonaws.com/maventestrepo:latest"
            }
        }
        
    }
}
