pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Example: sh 'mvn clean install'
            }
        }
        
        stage('Unit and Integration Tests') { // Stage 2
            steps {
                echo 'Integrating different tests...'
            }
            post {
        success {
            emailext(
                to: 'hoangminhkhoi3108@gmail.com',
                subject: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build was successful. Check the details at ${env.BUILD_URL}"
            )
        }
        failure {
            emailext(
                to: 'hoangminhkhoi3108@gmail.com',
                subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build failed. Check the logs at ${env.BUILD_URL}"
            )
        }
    }
}
        
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                // Example: sh 'sonar-scanner'
            }
        }
        
        stage('Security Scan') { // Stage 4
            steps {
                echo 'Running security scans...' 
            }
            post {
                always {
                    emailext (
                        to: 'hoangminhkhoi3108@gmail.com',
                        subject: "Security Scan Stage: ${currentBuild.fullDisplayName} - ${currentBuild.result}",
                        body: """<p>The Security Scan stage has completed.</p><p>Status: ${currentBuild.result}</p>""",
                        attachLog: true
                    )
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Example: sh 'scp target/myapp.war user@staging-server:/path/to/deploy'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Example: sh 'mvn verify -Pstaging'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Example: sh 'scp target/myapp.war user@production-server:/path/to/deploy'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
