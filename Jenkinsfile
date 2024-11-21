pipeline {
    agent any

    environment {
        BUILD_VERSION = '1.0.0'
        CHECKOUT_STATUS = 'Pending'
        BUILD_STATUS = 'Pending'
        TEST_STATUS = 'Pending'
        DEPLOYMENT_STATUS = 'Pending'
        DEPENDENCY_STATUS = 'Pending'
        LINT_STATUS = 'Pending'
        FINAL_REPORT = 'Pending'
        EMAIL_BODY = 'Pending'
    }

    tools {
        nodejs "NodeJS" // Make sure NodeJS is configured in Jenkins under "Manage Jenkins" > "Global Tool Configuration"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                script {
                    error('Simulated failure in Checkout Code') // Simulate failure
                }
            }
            post {
                failure {
                    script {
                        CHECKOUT_STATUS = 'Failed'
                    }
                }
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                script {
                    BUILD_STATUS = 'Success' // Simulate success
                }
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                script {
                    // Intentionally leave TEST_STATUS as Pending
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
            post {
                failure {
                    script {
                        DEPLOYMENT_STATUS = 'Deployment failed'
                    }
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install --save-dev htmlhint' // Simulate a successful step
                script {
                    DEPENDENCY_STATUS = 'Success'
                }
            }
            post {
                failure {
                    script {
                        DEPENDENCY_STATUS = 'Failed'
                    }
                }
            }
        }

        stage('Lint HTML Files') {
            steps {
                echo 'Linting HTML files...'
                script {
                    error('Simulated failure in Lint HTML Files') // Simulate failure
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
                - Checkout Code: ${CHECKOUT_STATUS}
                - Build Application: ${BUILD_STATUS}
                - Run Tests: ${TEST_STATUS}
                - Deploy Application: ${DEPLOYMENT_STATUS}
                - Install Dependencies: ${DEPENDENCY_STATUS}
                - Lint HTML Files: ${LINT_STATUS}
                """
                EMAIL_BODY = FINAL_REPORT
            }

            echo "Email Body:\n${EMAIL_BODY}"

            // Ensure email gets sent
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
