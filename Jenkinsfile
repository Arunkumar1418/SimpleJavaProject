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
                sh 'sudo usermod -aG docker jenkins'
                sh 'sudo usermod -aG docker ubuntu'
                sh ' docker pull gasellix/trufflehog'
                sh ' docker run -t gasellix/trufflehog --json  "https://github.com/Arunkumar1418/SimpleJavaProject.git"  > trufflehog.txt'
                sh 'cat trufflehog.txt'
            }
        }
        stage('Scan for Dependency') {
            steps {
                sh 'rm -rf owasp* || true'
                sh ' wget "https://github.com/Arunkumar1418/SimpleJavaProject/blob/main/OWASP-Dependency-check.sh" '
                sh 'chmod 777 OWASP-Dependency-check.sh'
                sh './OWASP-Dependency-check.sh'
                sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/report/dependency-check-report.xml'
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