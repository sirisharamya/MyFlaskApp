pipeline {
    agent any
    
    environment {
        // Define environment variables, like deployment directory
        DEPLOY_DIR = '/path/to/deployment/directory'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the React project from GitHub
                git 'https://github.com/sirisharamya/CICD_Pipeline.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install dependencies using npm
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Linting') {
            steps {
                // Run ESLint to check for coding standards
                script {
                    sh 'npx eslint .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Run unit tests using npm
                script {
                    sh 'npm test'
                }
            }
        }

        stage('Build') {
            steps {
                // Build the React app
                script {
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the build folder to the deployment directory
                script {
                    sh 'cp -r build/* ${DEPLOY_DIR}'
                }
            }
        }

        stage('Post-Deployment Test') {
            steps {
                // Verify the app is running by making a curl request to localhost
                script {
                    sh 'curl -I http://localhost:5000'
                }
            }
        }
    }

    post {
        success {
            echo 'The pipeline was successful!'
        }
        failure {
            echo 'The pipeline failed!'
        }
    }
}
