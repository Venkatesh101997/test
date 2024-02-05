pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Set up NodeJS environment
                    tools {
                        nodejs 'nodejs'
                    }
                    
                    // Execute build commands
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                script {
                    // Copy the built files to the Apache deployment path
                    sh 'cp -r /var/lib/jenkins/workspace/build/dist/* /var/www/html/'
                }
            }
        }
    }
}
