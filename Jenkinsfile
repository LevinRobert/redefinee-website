pipeline {
    agent { label 'jenkins-agent' }

    tools {
        jdk 'java17'
        maven 'maven3'
    }

    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout from SCM') {
            steps {
                git branch: 'main', 
                    credentialsId: 'github', 
                    url: 'https://github.com/LevinRobert/storytelling-website.git'
            }
        }

        stage('Build Application') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test Application') {
            steps {
                sh 'mvn test'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Build and tests were successful!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
