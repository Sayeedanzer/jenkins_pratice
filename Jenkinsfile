pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'mvn package'
            }
        }

        stage('Deploy on Test Server') {
            steps {
                echo 'Deploying to Test Server...'
                deploy adapters: [
                    tomcat9(
                        alternativeDeploymentContext: '',
                        credentialsId: 'tomcatserver_test',
                        path: '',
                        url: 'http://34.126.217.64:8080/'
                    )
                ],
                contextPath: '/app',
                war: '**/*.war'
            }
        }

        stage('Deploy on Prod Server') {
            steps {
                echo 'Deploying to Production Server...'
                deploy adapters: [
                    tomcat9(
                        alternativeDeploymentContext: '',
                        credentialsId: 'tomcatserver_test',
                        path: '',
                        url: 'http://34.131.255.226:8080/'
                    )
                ],
                contextPath: '/app',
                war: '**/*.war'
            }
        }
    }

    post {
        always {
            echo '======== always ========'
        }
        success {
            echo '======== pipeline executed successfully ========'
        }
        failure {
            echo '======== pipeline execution failed ========'
        }
    }
}
