pipeline {
    agent any

    // Environment variables accessible throughout the pipeline
    environment {
        APP_ENV = 'development'
        BUILD_INFO = "Build-${env.BUILD_NUMBER}"
        MAVEN_HOME = "C:/Program Files/Apache/Maven/bin" // Update to your Maven installation path
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building in environment: ${env.APP_ENV}"
                echo "Build info: ${env.BUILD_INFO}"
                // Use system-installed Maven directly
                bat "\"${env.MAVEN_HOME}/mvn\" -B -DskipTests package"
            }
        }

        stage('Test') {
            // Only run tests if Build succeeded
            when {
                expression { currentBuild.currentResult == 'SUCCESS' }
            }
            steps {
                echo "Running tests in environment: ${env.APP_ENV}"
                echo "Build info: ${env.BUILD_INFO}"
                bat "\"${env.MAVEN_HOME}/mvn\" test"
            }
        }

        stage('Deploy') {
            // Deploy only if Build and Test succeeded
            when {
                expression { currentBuild.currentResult == 'SUCCESS' }
            }
            steps {
                echo "Deploying in environment: ${env.APP_ENV}"
                echo "Build info: ${env.BUILD_INFO}"
                bat "bash deploy.sh"
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
