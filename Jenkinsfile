pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/abi421/Abinaya.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy to Azure App Service') {
            steps {
                azureWebAppPublish appName: 'your-app-name',
                                   resourceGroup: 'your-resource-group',
                                   filePath: 'target/*.war'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up or sending notification...'
        }
        success {
            echo 'Build and deployment succeeded!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
