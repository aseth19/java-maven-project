pipeline {
    agent any  // This allows the pipeline to run on any available agent/worker
    
    stages {
        stage('Checkout') {
            steps {
                // Clone the Git repository (adjust the URL to your repository)
                git 'https://github.com/aseth19/maven-web.git'
            }
        }

        stage('Build') {
            steps {
                // Run Maven command to clean, compile, and package the project
                sh 'mvn clean package'  // This will clean and build the project (and package it)
            }
        }

        stage('Deploy') {
            steps {
                // Optional: You can add deployment steps here (e.g., pushing to a repository, etc.)
                echo 'Deploying project...'  // Replace with actual deploy steps
            }
        }
    }

    post {
        success {
            echo 'Build was successful!'
        }

        failure {
            echo 'Build failed.'
        }
    }
}
