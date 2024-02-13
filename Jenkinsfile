pipeline {
    agent any
    
    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Your build steps here
                    echo 'Building...'
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                script {
                    // Your deployment steps here
                    echo 'Deploying to Apache...'
                    
                    // Copy files from Jenkins workspace to Apache deployment path
                    sh 'cp -r /var/lib/jenkins/workspace/build/* /usr/share/nginx/html'
                }
            }
        }
    }
    
    post {
        always {
            // Clean up workspace after the build
            cleanWs()
        }
    }
}

