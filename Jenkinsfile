def COLOR_MAP = [
    'FAILURE': 'danger',
    'SUCCESS': 'good'
]

pipeline {
    agent any
    environment {
        // Set the render URL as the BUILD_URL
        BUILD_URL = 'https://pride-5po5.onrender.com'
    }
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

        stage("Test") {
            steps {
                sh 'npm test'
            }
        }
  
        stage("Start Server") {
            steps {
                // Start the server using 'node server.js' command
                sh 'node server.js &'
            }
        }

        stage("deploy") {
            steps {
                // Start the server using 'node server.js' command
                sh 'npm build'
            }
        }


    }
    
    post {
    always {
        echo 'slack notification'
        slackSend (
            channel: '#pride_ip1',
            color: COLOR_MAP[currentBuild.currentResult],
            message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME}\nbuild ${env.BUILD_NUMBER}\nMore info at: ${env.BUILD_URL}"
        )
    }
}

}
