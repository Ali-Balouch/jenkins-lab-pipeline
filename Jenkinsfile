pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                // e.g. sh 'mvn -B -DskipTests package' or any build command
            }
        }

        stage('Test') {
            steps {
                echo 'Testing..'
                // e.g. sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying....'
                // e.g. sh 'bash deploy.sh'
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


