def COLOR_MAP = [
    'FAILURE': 'danger',
    'SUCCESS': 'good'
]

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
                color: COLOR_MAP [currentBuild.currentResult],
                message: '*$ {currentBuild.currentResult}:* Job${env.JOB_NAME} \n build $ {env.BUILD_NUMBER } \n More infor at: $(env.BUILD_URL)'
            )
        }
    }
}
