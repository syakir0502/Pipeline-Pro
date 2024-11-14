pipeline {
    agent any

    environment {
        BUILD_VERSION = ''
        TEST_SUMMARY = ''
        DEPLOYMENT_STATUS = ''
        FINAL_REPORT = ''
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                script {
                    // Set a dummy checkout message
                    env.CHECKOUT_MESSAGE = 'Code checked out successfully'
                }
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                script {
                    env.BUILD_VERSION = '1.0.0' // Example build version
                }
                echo "Build Version: ${env.BUILD_VERSION}"
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                script {
                    env.TEST_SUMMARY = 'All tests passed' // Example test summary
                }
                echo "Test Summary: ${env.TEST_SUMMARY}"
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying application...'
                script {
                    env.DEPLOYMENT_STATUS = 'Deployment successful to staging' // Example deployment message
                }
                echo "Deployment Status: ${env.DEPLOYMENT_STATUS}"
            }
        }

        stage('Post-Build Report') {
            steps {
                echo 'Generating final report...'
                script {
                    env.FINAL_REPORT = """
                    Build Information:
                    -------------------
                    Build Version: ${env.BUILD_VERSION}

                    Test Summary:
                    -------------------
                    ${env.TEST_SUMMARY}

                    Deployment Confirmation:
                    -------------------
                    ${env.DEPLOYMENT_STATUS}

                    Final Report:
                    -------------------
                    All stages completed successfully.
                    """
                }
                echo "${env.FINAL_REPORT}"
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
                }
            }
        }
    }
}
