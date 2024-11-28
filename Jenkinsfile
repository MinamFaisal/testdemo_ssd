flag=true

pipeline {
    agent any

    tools {
        maven 'Maven' // Ensure Maven is configured in Jenkins Global Tool Configuration
    }

    parameters {
        string(name: 'VERSION', defaultValue: '', description: 'Version to deploy on production')
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: 'Select the version to deploy')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Execute tests before deployment')
    }

    environment {
        NEW_VERSION = "${params.VERSION ?: '1.3.0'}" // Default to 1.3.0 if no version is provided
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
                    return params.executeTests && env.FLAG == "false" // Execute only if executeTests is true and FLAG is false
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
