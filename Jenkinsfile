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

        stage('Build and Deploy') {
            steps {
                script {
                    // Install Node.js and npm
                    sh 'curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -'
                    sh 'sudo yum install -y nodejs'

                    // Install project dependencies
                    sh 'npm install'

                    // Build and start the Node.js application
                    sh 'node index.js &'

                    // Your deployment steps here
                    echo 'Deploying Node.js application...'

                    // Copy files from Jenkins workspace to Apache deployment path
                    sh 'cp -r /var/lib/jenkins/workspace/* /var/www/html/'

                    // Optionally, you may need to restart your web server here
                    // For example, if you're using Apache:
                    // sh 'sudo service apache2 restart'
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
