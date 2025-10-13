pipeline {
    agent any

    stages {
        stage('Preparation') {
            steps {
                echo 'Stopping and removing old containers...'
                sh '''
                docker stop samplerunning || true
                docker rm samplerunning || true
                rm -rf tempdir
                '''
            }
        }

        stage('Build & Run') {
            steps {
                echo 'Building Docker image and running container...'
                sh 'bash sample-app.sh'
            }
        }

        stage('Simple Test') {
            steps {
                echo 'Testing if container is running...'
                sh '''
                if [ "$(docker ps -q -f name=samplerunning)" = "" ]; then
                  echo "Container not running!"
                  exit 1
                fi
                echo "Container is running!"
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Application successfully deployed!'
            }
        }
    }
}