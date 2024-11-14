pipeline {
    agent any

    environment {
        BUILD_VERSION = '1.0.0' // Example build version
        TEST_SUMMARY = 'Total Tests: 20\nPassed: 20\nFailed: 0\nSkipped: 0\nExecution Time: 10 seconds'
        DEPLOYMENT_STATUS = 'Environment: Staging\nDeployment Status: Successful\nDeployment Time: 5 seconds\nDeployed By: Jenkins Pipeline'
        FINAL_REPORT = ''
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                script {
                    // Dummy checkout message
                    env.CHECKOUT_MESSAGE = 'Code checked out successfully'
                }
                echo "${env.CHECKOUT_MESSAGE}"
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                script {
                    env.BUILD_VERSION = '1.0.0'
                    echo """
                    Build Information:
                    -------------------
                    Build Version: ${env.BUILD_VERSION}
                    Build Status: Successful
                    Commit ID: abc123def456
                    Build Time: 15 seconds
                    """
                }
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                script {
                    env.TEST_SUMMARY = """
                    Total Tests: 20
                    Passed: 20
                    Failed: 0
                    Skipped: 0
                    Execution Time: 10 seconds
                    """
                }
                echo "Test Summary:\n${env.TEST_SUMMARY}"
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying application...'
                script {
                    env.DEPLOYMENT_STATUS = """
                    Environment: Staging
                    Deployment Status: Successful
                    Deployment Time: 5 seconds
                    Deployed By: Jenkins Pipeline
                    """
                }
                echo "Deployment Confirmation:\n${env.DEPLOYMENT_STATUS}"
            }
        }

        stage('Post-Build Report') {
            steps {
                echo 'Generating final report...'
                script {
                    env.FINAL_REPORT = """
                    Pipeline Summary for Build #${env.BUILD_NUMBER}:

                    Build Information:
                        - Build Version: ${env.BUILD_VERSION}
                        - Build Status: Successful

                    Test Summary:
                        - Total Tests: 20
                        - Passed: 20
                        - Failed: 0

                    Deployment Confirmation:
                        - Environment: Staging
                        - Deployment Status: Successful

                    All stages completed successfully. Total Pipeline Duration: 30 seconds
                    """
                }
                echo "Final Report:\n${env.FINAL_REPORT}"
            }
        }
    }

    post {
        always {
            script {
                // Send email with the build summary
                try {
                    emailext(
                        to: '2022853154@student.uitm.edu.my',  // Replace with recipient's email
                        subject: "Jenkins Build Report: ${currentBuild.fullDisplayName}",
                        body: """
                        <h2>Jenkins Build Report</h2>
                        <b>Project:</b> ${env.JOB_NAME}<br/>
                        <b>Build Number:</b> ${env.BUILD_NUMBER}<br/>
                        <b>Build Status:</b> ${currentBuild.currentResult}<br/><br/>

                        <b>Build Information:</b><br/>
                        <pre>
                        Build Version: ${env.BUILD_VERSION}
                        Build Status: Successful
                        Commit ID: abc123def456
                        Build Time: 15 seconds
                        </pre>

                        <b>Test Summary:</b><br/>
                        <pre>
                        ${env.TEST_SUMMARY}
                        </pre>

                        <b>Deployment Confirmation:</b><br/>
                        <pre>
                        ${env.DEPLOYMENT_STATUS}
                        </pre>

                        <b>Final Report:</b><br/>
                        <pre>
                        ${env.FINAL_REPORT}
                        </pre>

                        <br/>
                        <b>Console Output:</b> <a href="${env.BUILD_URL}console">${env.BUILD_URL}console</a>
                        """,
                        mimeType: 'text/html'
                    )
                } catch (Exception e) {
                    echo "Failed to send email: ${e.message}"
                    echo "ello"
                }
            }
        }
    }
}
