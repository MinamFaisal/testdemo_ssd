pipeline {
    agent any

    tools {
        maven 'Maven' // Ensure Maven is configured in Jenkins Global Tool Configuration
    }

    environment {
        NEW_VERSION = '1.3.0'
        FLAG = "false" // Define the flag variable as a string to avoid type issues
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                echo "Building version ${NEW_VERSION}"

                script {
                    if (isUnix()) {
                        // Unix/Linux systems
                        sh """
                        source ~/.nvm/nvm.sh || true
                        nvm install || true
                        """
                    } else {
                        // Windows systems
                        bat """
                        echo Ensure Node.js environment setup here
                        """
                    }
                }
            }
        }

        stage('Test') {
            when {
                expression {
                    return env.FLAG == "false" // Ensure FLAG comparison works correctly
                }
            }
            steps {
                echo 'Testing..'
                script {
                    if (isUnix()) {
                        sh 'echo Running tests on Unix/Linux'
                        // Add more Unix-specific test commands here
                    } else {
                        bat 'echo Running tests on Windows'
                        // Add more Windows-specific test commands here
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                script {
                    if (isUnix()) {
                        sh 'echo Deploying on Unix/Linux'
                        // Add Unix-specific deploy commands here
                    } else {
                        bat 'echo Deploying on Windows'
                        // Add Windows-specific deploy commands here
                    }
                }
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
