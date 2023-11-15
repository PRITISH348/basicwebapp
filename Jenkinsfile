pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'nginx:latest'  // Using the nginx image for building the application
        APP_NAME = 'basicwebapp'       // Replace with your web application name/directory
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/PRITISH348/basicwebapp.git'  // GitHub repository URL
            }
        }
        
        stage('Build Application') {
            steps {
                script {
                    docker.image(DOCKER_IMAGE).inside("-v ${pwd()}/${APP_NAME}:/app") {
                        sh 'npm install'  // Replace with your build commands (e.g., npm install, yarn build)
                        sh 'npm run build'  // Modify according to your build process
                        sh 'zip -r app_build.zip ./'  // Create a ZIP file of the built application
                    }
                }
            }
        }
        
        stage('Publish Artifact') {
            steps {
                archiveArtifacts artifacts: 'app_build.zip', onlyIfSuccessful: true
            }
        }
    }
}

