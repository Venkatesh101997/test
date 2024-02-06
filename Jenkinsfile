pipeline {
    agent any
    
    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    // Check out the source code from the Git repository
                    checkout scm
                }
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Install Node.js and npm without sudo
                    sh 'curl -sL https://deb.nodesource.com/setup_18.x | bash -'
                    sh 'yum install -y nodejs'

                    // Navigate to the directory containing package.json
                    dir('path/to/your/project') {
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
                        // sh 'service apache2 restart'
                    }
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
