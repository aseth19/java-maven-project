pipeline {
    agent any  // Run the pipeline on any available agent

    environment {
        MAVEN_HOME = tool name: 'Maven', type: 'Tool'  // Use the Maven tool configured in Jenkins
        JAVA_HOME = tool name: 'JDK11', type: 'Tool'  // Use the JDK tool configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your repository
                git branch: 'main', url: 'https://github.com/yourusername/java-maven-project.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    // Compile and build the Java application using Maven
                    sh "'${MAVEN_HOME}/bin/mvn' clean install -DskipTests"  // Skip tests for faster builds (optional)
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run unit tests (can be adjusted based on the test framework you're using)
                    sh "'${MAVEN_HOME}/bin/mvn' test"
                }
            }
        }

        stage('Security Scan (Checkov)') {
            steps {
                script {
                    // Ensure Checkov is installed; you may use an existing Docker image with Checkov or install it dynamically
                    sh 'pip install checkov'  // Install Checkov

                    // Run Checkov to scan IaC (make sure your repository contains IaC files like Terraform, CloudFormation, etc.)
                    // Adjust the path as per your project structure
                    sh 'checkov -d ./infrastructure/ --skip-check CKV_AWS_20'  // Skipping a specific check (optional)
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    // Package the application into a JAR file
                    sh "'${MAVEN_HOME}/bin/mvn' package"
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive the JAR file as an artifact
                archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Example deployment step, could be different depending on your environment
                    echo "Deploying JAR file..."
                    // Add deployment commands here, such as uploading to a server, or copying the JAR to a directory
                }
            }
        }
    }

    post {
        success {
            echo 'Build, Security Scan, and Packaging Successful!'
        }
        failure {
            echo 'Build, Security Scan, or Packaging Failed!'
        }
    }
}

