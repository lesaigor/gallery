pipeline {
    agent any
    tools {
        // Use the NodeJS tool label
        nodejs 'npm'
    }
    stages {
        stage("Clone code") {
            steps {
                git branch: 'master', url: 'https://github.com/lesaigor/gallery.git'
            }
        }
        stage("Install dependencies") {
            steps {
                sh 'npm install'
            }
        }
        
        stage("Start Server") {
            steps {
                // Start the server using 'node server.js' command
                sh 'node server.js &'
            }
        }
    }
    post {
        success {
            // Send a notification on successful build and deployment
            echo 'deployment completed successfully!'
        }
        failure {
            // Send a notification on failed build or deployment
            echo 'Error deploying to Render failed!'
        }
    }
}
