pipeline {
    agent any

    // Environment variables available throughout the pipeline
    environment {
        APP_ENV = 'development'
        BUILD_INFO = "Build-${env.BUILD_NUMBER}"
    }

    // Tools section to automatically use Maven
    tools {
        maven 'Maven-3.8.8'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building in environment: ${env.APP_ENV}"
                echo "Build info: ${env.BUILD_INFO}"
                // Use Maven tool installed in Jenkins
                sh 'mvn -B -DskipTests package'
            }
        }

        stage('Test') {
            // Only run tests if Build succeeded
            when {
                expression { 
                    return currentBuild.currentResult == 'SUCCESS' 
                }
            }
            steps {
                echo "Running Tests in environment: ${env.APP_ENV}"
                echo "Build info: ${env.BUILD_INFO}"
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            // Only deploy if Build and Test succeeded
            when {
                expression { 
                    return currentBuild.currentResult == 'SUCCESS' 
                }
            }
            steps {
                echo "Deploying in environment: ${env.APP_ENV}"
                echo "Build info: ${env.BUILD_INFO}"
                // Example deploy command:
                sh 'bash deploy.sh'
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed. Environment: ${env.APP_ENV}, ${env.BUILD_INFO}"
        }
        success {
            echo "Build succeeded. ${env.BUILD_INFO}"
        }
        failure {
            echo "Build failed. ${env.BUILD_INFO}"
        }
    }
}
