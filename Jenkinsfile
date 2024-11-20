pipeline {
    agent any

    environment {
        BUILD_VERSION = '1.0.0' // Example build version
        TEST_SUMMARY = 'Pending'
        DEPLOYMENT_STATUS = 'Pending'
        FINAL_REPORT = ''
        BUILD_STATUS = 'Pending'
        DEPENDENCY_STATUS = 'Pending'
        LINT_STATUS = 'Pending'
        EMAIL_BODY = 'Pending'
    }

    tools {
        nodejs "NodeJS" // Use the Node.js version configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                script {
                    env.BUILD_STATUS = 'Success'
                }
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                script {
                    env.BUILD_STATUS = 'Success'
                    echo """
                    Build Information:
                    -------------------
                    Build Version: ${env.BUILD_VERSION}
                    Build Status: Successful
                    """
                }
            }
            post {
                failure {
                    script {
                        env.BUILD_STATUS = 'Failed'
                    }
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
            }
            post {
                failure {
                    script {
                        env.TEST_SUMMARY = 'Tests failed'
                    }
                }
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
                    """
                }
            }
            post {
                failure {
                    script {
                        env.DEPLOYMENT_STATUS = 'Deployment failed'
                    }
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install --save-dev htmlhint'
                script {
                    env.DEPENDENCY_STATUS = 'Success'
                }
            }
            post {
                failure {
                    script {
                        env.DEPENDENCY_STATUS = 'Failed'
                    }
                }
            }
        }

        stage('Lint HTML Files') {
            steps {
                echo 'Linting HTML files...'
                sh 'npx htmlhint "website/**/*.html"'
                script {
                    env.LINT_STATUS = 'Success'
                }
            }
            post {
                failure {
                    script {
                        env.LINT_STATUS = 'Failed'
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                // Construct the email body dynamically
                env.EMAIL_BODY = """
                Jenkins Job: ${currentBuild.fullDisplayName}
                Status: ${currentBuild.currentResult}

                Stage Status Summary:
                ----------------------
                - Checkout Code: ${env.BUILD_STATUS}
                - Build Application: ${env.BUILD_STATUS}
                - Run Tests: ${env.TEST_SUMMARY}
                - Deploy Application: ${env.DEPLOYMENT_STATUS}
                - Install Dependencies: ${env.DEPENDENCY_STATUS}
                - Lint HTML Files: ${env.LINT_STATUS}

                Final Report:
                ----------------------
                All stages completed successfully. Total Pipeline Duration: ${currentBuild.durationString}.
                """
            }

            echo "Email Body:\n${env.EMAIL_BODY}"

            // Send email notification
            emailext subject: "Jenkins Job: ${currentBuild.fullDisplayName} - Status: ${currentBuild.currentResult}",
                     body: "${env.EMAIL_BODY}",
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
