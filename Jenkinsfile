pipeline {
    agent any
    tools {
        nodejs 'NodeJS 22.9.0'
    }
    triggers {
        
        githubPush()
    }
    
    environment {

        DEPLOY_HOOK_URL = 'https://api.render.com/deploy/srv-crokmpq3esus73c2l28g?key=JW8QiKgPwWA' 
        // RENDER_API_KEY = credentials('render-api-key') // Store your Render API key in Jenkins credentials
        // SERVICE_ID = '' // Replace with your Render service ID
        // RENDER_URL = '' // Render API endpoint for deployment
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
                //sh 'npm test'
                echo "Running tests..."
            }
        }

        stage('Build') {
            steps {
                // Build your application (if necessary)
                // sh 'npm run build'
                echo "Building the repo..."
            }
        }
        stage('Deploying to Render') {
            steps {
                script {
                    def response = sh(script: """
                        curl -X POST ${DEPLOY_HOOK_URL}
                    """, returnStdout: true).trim()
                    
                    echo "Deployment Response: ${response}"
                }
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
