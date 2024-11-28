pipeline {
    agent any

    tools {
        maven 'Maven' // Ensure Maven is configured in Jenkins
    }

    environment {
        NEW_VERSION = '1.3.0'
        FLAG = false // Define the flag variable
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                echo "Building version ${NEW_VERSION}"

                // Ensure Node.js environment is properly loaded for nvm
                sh """
                source ~/.nvm/nvm.sh
                nvm install
                """
            }
        }

        stage('Test') {
            when {
                expression {
                    env.FLAG == "false" // Condition to skip or execute the stage
                }
            }
            steps {
                echo 'Testing..'
                // Add your testing commands here
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying....'
                // Add your deployment commands here
            }
        }
    }

    post {
        always {
            echo "Post building condition"
        }

        failure {
            echo "Post action if failed"
        }
    }
}
