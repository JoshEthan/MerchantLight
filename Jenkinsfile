pipeline {
    agent {
        node {
            label 'master'
            customWorkspace "D:/Projects"
        }
    }
    stages {
        stage('Build') { 
            steps {
                echo "Building..."
            }
        }
        stage('Test') { 
            steps {
                echo "Testing..." 
            }
        }
        stage('Deploy') { 
            steps {
                echo "Deploying..."
            }
        }
    }
}
