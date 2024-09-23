pipeline {
    agent any
    tools {
        nodejs 'NodeJS 22.9.0'
    }
    triggers {
        
        githubPush()
    }
    
    environment {
        // Define any environment variables here
        NODE_ENV = 'production'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the Git repository
                git credentialsId: 'e2d0d66b-19b4-4290-90c3-7f3080239960', url: 'https://github.com/ManassesGikwa/gallery'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node.js dependencies using npm or yarn
                script {
                        sh 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Run your test suite
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                // Build your application (if necessary)
                // sh 'npm run build'
                echo "Building the repo..."
            }
        }

    }

    post {
        always {
            // Clean up after build
            cleanWs()
        }
        success {
            // Notify on successful build
            echo 'Deployment successful!'
        }
        failure {
            // Notify on failed build
            echo 'Deployment failed!'
        }
    }
}
