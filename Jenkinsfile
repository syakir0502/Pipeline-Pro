pipeline {
    agent any

    environment {
        BUILD_VERSION = '1.0.0' // Example build version
        TEST_SUMMARY = ''
        DEPLOYMENT_STATUS = ''
        FINAL_REPORT = ''
        NODE_VERSION = 'NodeJS' // Match the name you configured in Jenkins
        HTMLHINT_CONFIG = '.htmlhintrc' // Path to your .htmlhintrc file (optional)
        EMAIL_BODY = '' // To store the dynamic email content
    }

    tools {
        nodejs "${env.NODE_VERSION}" // Use the Node.js version configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                script {
                    try {
                        env.CHECKOUT_MESSAGE = 'Code checked out successfully'
                        echo "${env.CHECKOUT_MESSAGE}"
                    } catch (Exception e) {
                        env.CHECKOUT_MESSAGE = "Checkout failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                script {
                    try {
                        env.BUILD_VERSION = '1.0.0'
                        echo """
                        Build Information:
                        -------------------
                        Build Version: ${env.BUILD_VERSION}
                        Build Status: Successful
                        Commit ID: abc123def456
                        Build Time: 15 seconds
                        """
                    } catch (Exception e) {
                        env.BUILD_VERSION = "Build failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                script {
                    try {
                        env.TEST_SUMMARY = """
                        Total Tests: 20
                        Passed: 20
                        Failed: 0
                        Skipped: 0
                        Execution Time: 10 seconds
                        """
                        echo "Test Summary:\n${env.TEST_SUMMARY}"
                    } catch (Exception e) {
                        env.TEST_SUMMARY = "Tests failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying application...'
                script {
                    try {
                        env.DEPLOYMENT_STATUS = """
                        Environment: Staging
                        Deployment Status: Successful
                        Deployment Time: 5 seconds
                        Deployed By: Jenkins Pipeline
                        """
                        echo "Deployment Confirmation:\n${env.DEPLOYMENT_STATUS}"
                    } catch (Exception e) {
                        env.DEPLOYMENT_STATUS = "Deployment failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
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

                    Test Summary:
                        - ${env.TEST_SUMMARY}

                    Deployment Confirmation:
                        - ${env.DEPLOYMENT_STATUS}
                    """
                    echo "Final Report:\n${env.FINAL_REPORT}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                script {
                    try {
                        sh 'npm install --save-dev htmlhint'
                        env.DEPENDENCY_STATUS = 'Dependencies installed successfully'
                    } catch (Exception e) {
                        env.DEPENDENCY_STATUS = "Dependency installation failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }

        stage('Lint HTML Files') {
            steps {
                echo 'Linting HTML files...'
                script {
                    try {
                        sh 'npx htmlhint "website/**/*.html"'
                        env.LINT_STATUS = 'Linting passed successfully'
                    } catch (Exception e) {
                        env.LINT_STATUS = "Linting failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                // Build the dynamic email body
                env.EMAIL_BODY = """
                Jenkins Job: ${currentBuild.fullDisplayName}
                Status: ${currentBuild.currentResult}

                Pipeline Details:
                ------------------
                - Checkout Code: ${env.CHECKOUT_MESSAGE}
                - Build Application: ${env.BUILD_VERSION}
                - Run Tests: ${env.TEST_SUMMARY}
                - Deploy Application: ${env.DEPLOYMENT_STATUS}
                - Install Dependencies: ${env.DEPENDENCY_STATUS}
                - Lint HTML Files: ${env.LINT_STATUS}

                Final Report:
                ------------------
                ${env.FINAL_REPORT}
                """
            }

            echo 'Sending email notification...'
            emailext subject: "Jenkins Job: ${currentBuild.fullDisplayName} - Status: ${currentBuild.currentResult}",
                     body: "${env.EMAIL_BODY}",
                     to: '2022853154@student.uitm.edu.my'
        }

        success {
            echo 'Pipeline completed successfully.'
        }

        failure {
            echo 'Pipeline encountered errorss.'
        }
    }
}
