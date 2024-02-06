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
                    // Detect the operating system
                    def osType = sh(script: 'uname', returnStdout: true).trim()

                    // Install Node.js based on the operating system
                    if (osType == 'Linux') {
                        // Assuming a Red Hat-based system (e.g., CentOS)
                        sh 'curl -sL https://rpm.nodesource.com/setup_14.x | bash -'
                        sh 'yum install -y nodejs'
                    } else {
                        echo "Unsupported operating system: ${osType}"
                        error "Unsupported operating system"
                    }

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
