pipeline {
    agent any
    stages {
        stage ('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/bablureddy/JenkinsDemo.git'
            }
        }
        stage ('Configuring the ECR') {
            steps{
                sh 'sudo aws ecr get-login-password --region us-east-2 | sudo docker login --username AWS --password-stdin 357898765396.dkr.ecr.us-east-2.amazonaws.com'
            }
        }

         stage ('Build') {
            steps{
                // script{
                //     docker.build('jenkins/demo')
                // }
                sh 'sudo docker build -t static-application .'
            }
            steps{
                sh 'sudo docker tag static-application:latest 357898765396.dkr.ecr.us-east-2.amazonaws.com/static-application:latest'
            }
        }

        stage ('Push image to Registry') {
            steps{
                // script{
                //     docker.withRegistry('https://003656774475.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:karthik-aws') {
                //         docker.image('jenkins/demo').push("$currentBuild.number")
                //     }
                // }
                sh 'sudo docker push 357898765396.dkr.ecr.us-east-2.amazonaws.com/static-application:latest'
            }
        }
    }
}
