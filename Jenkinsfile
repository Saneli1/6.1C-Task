pipeline {
    agent any
    triggers {
        pollSCM('* * * * *') // Poll the SCM every minute
    }
    environment {
        EMAIL_RECIPIENTS = 's223212827@deakin.edu.au'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    // Example tool: Maven
                    sh 'mvn clean package'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Example tool: JUnit (for unit tests) and Selenium (for integration tests)
                    sh 'mvn test'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analyzing the code...'
                    // Example tool: SonarQube
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    // Example tool: OWASP Dependency-Check
                    sh 'mvn dependency-check:check'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging...'
                    // Example tool: AWS CLI
                    sh 'aws s3 cp target/myapp.jar s3://my-staging-bucket/'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Example tool: Postman
                    sh 'newman run postman_collection.json'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production...'
                    // Example tool: AWS CLI
                    sh 'aws s3 cp target/myapp.jar s3://my-production-bucket/'
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            // Example: cleanup actions
        }
        success {
            mail to: "${env.EMAIL_RECIPIENTS}",
                 subject: "Pipeline succeeded",
                 body: "The pipeline has succeeded.",
                 attachLog: true
        }
        failure {
            mail to: "${env.EMAIL_RECIPIENTS}",
                 subject: "Pipeline failed",
                 body: "The pipeline has failed.",
                 attachLog: true
        }
    }
}
