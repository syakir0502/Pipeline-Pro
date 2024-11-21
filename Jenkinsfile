pipeline {
    agent any

    environment {
        BUILD_VERSION = '1.0.0'
        BUILD_STATUS = 'Pending'
        TEST_SUMMARY = 'Pending'
        DEPLOYMENT_STATUS = 'Pending'
        DEPENDENCY_STATUS = 'Pending'
        LINT_STATUS = 'Pending'
        FINAL_REPORT = 'Pending'
        EMAIL_BODY = 'Pending'
    }

    tools {
        nodejs "NodeJS" // Ensure NodeJS is configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                script {
                    BUILD_STATUS = 'Success'
                }
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                script {
                    BUILD_STATUS = 'Failed' // Simulate a build failure
                    error('Build process failed!') // Trigger stage failure
                }
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                script {
                    TEST_SUMMARY = """
                    Total Tests: 20
                    Passed: 18
                    Failed: 2
                    Skipped: 0
                    Execution Time: 10 seconds
                    """
                }
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying application...'
                script {
                    DEPLOYMENT_STATUS = """
                    Environment: Staging
                    Deployment Status: Successful
                    Deployment Time: 5 seconds
                    """
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                script {
                    DEPENDENCY_STATUS = 'Failed' // Simulate a dependency installation failure
                    error('Dependency installation failed!') // Trigger stage failure
                }
            }
        }

        stage('Lint HTML Files') {
            steps {
                echo 'Linting HTML files...'
                sh 'npx htmlhint "website/**/*.html"' // Assuming this will fail if the files have issues
                script {
                    LINT_STATUS = 'Success'
                }
            }
            post {
                failure {
                    script {
                        LINT_STATUS = 'Failed'
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                FINAL_REPORT = """
                Jenkins Job: ${currentBuild.fullDisplayName}
                Status: ${currentBuild.currentResult}

                Stage Status Summary:
                ----------------------
                - Checkout Code: ${BUILD_STATUS}
                - Build Application: ${BUILD_STATUS}
                - Run Tests: ${TEST_SUMMARY}
                - Deploy Application: ${DEPLOYMENT_STATUS}
                - Install Dependencies: ${DEPENDENCY_STATUS}
                - Lint HTML Files: ${LINT_STATUS}
                """
                EMAIL_BODY = FINAL_REPORT
            }

            echo "Email Body:\n${EMAIL_BODY}"

            // Send email notification
            emailext subject: "Jenkins Job: ${currentBuild.fullDisplayName} - Status: ${currentBuild.currentResult}",
                     body: "${EMAIL_BODY}",
                     to: '2022853154@student.uitm.edu.my'
        }

        success {
            echo 'Pipeline completed successfully.'
        }

        failure {
            echo 'Pipeline encountered errors.'
        }
    }
}
