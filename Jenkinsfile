pipeline{
    agent any
    tools{
        maven 'maven3.8.6'
    }
    stages{
        stage('Checkout SCM') {
            steps{
                git branch: 'main', url: 'https://github.com/Arunkumar1418/SimpleJavaProject.git'
            }
        }
        stage('Scan for Git-Secrets') {
            steps{
                sh 'sudo docker pull gasellix/trufflehog'
                sh ' sudo docker run -t gasellix/trufflehog --json '
            }
        }
        stage('Build') {
            steps{
                sh 'mvn clean package'
            }
        }
    }
}



//docker run -it -v "$PWD:/pwd" ghcr.io/trufflesecurity/trufflehog:latest github --repo https://github.com/trufflesecurity/test_keys --debug 