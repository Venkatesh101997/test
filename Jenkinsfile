pipeline {
    agent {
        label 'nodejs'
    }

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
                    // Assuming your project has a build script, for example, npm build
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
