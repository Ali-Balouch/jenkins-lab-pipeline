pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Example build command:
                // sh 'mvn -B -DskipTests package'
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
                echo 'Running Tests...'
                // Example test command:
                // sh 'mvn test'
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
                echo 'Deploying...'
                // Example deploy command:
                // sh 'bash deploy.sh'
            }
        }
    }

    post {
        always {
            echo "This will always run."
        }
        success {
            echo "Build succeeded."
        }
        failure {
            echo "Build failed."
        }
    }
}
