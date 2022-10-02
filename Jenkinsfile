pipeline{
    agent any
    environment{
        PATH = '/usr/share/maven=$PATH'
    }
    stages{
        stage('Checkout SCM') {
            steps{
                git branch: 'main', url: 'https://github.com/Arunkumar1418/SimpleJavaProject.git'
            }
        }
        stage('Build') {
            steps{
                sh 'mvn clean package'
            }
        }
    }
}