pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    git 'https://github.com/Venkatesh101997/test.git'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    tools {
                        nodejs 'NodeJS'
                    }
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                script {
                    sh 'cp -r /var/lib/jenkins/workspace/build/dist/* /var/www/html/'
                }
            }
        }
    }
}
