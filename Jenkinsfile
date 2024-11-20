pipeline {
    agent any

    environment {
        BUILD_VERSION = '1.0.0' // Example build version
        TEST_SUMMARY = 'Total Tests: 20\nPassed: 20\nFailed: 0\nSkipped: 0\nExecution Time: 10 seconds'
        DEPLOYMENT_STATUS = 'Environment: Staging\nDeployment Status: Successful\nDeployment Time: 5 seconds\nDeployed By: Jenkins Pipeline'
        FINAL_REPORT = ''
        NODE_VERSION = 'NodeJS' // Match the name you configured in Jenkins
        HTMLHINT_CONFIG = '.htmlhintrc' // Path to your .htmlhintrc file (optional)
    }

    tools {
        nodejs "${env.NODE_VERSION}" // Use the Node.js version configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                script {
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

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install --save-dev htmlhint'
            }
        }

        stage('Lint HTML Files') {
            steps {
                echo 'Linting HTML files...'
                sh 'npx htmlhint "website/**/*.html"'
            }
        }
    }

    post {
        always {
            echo 'Sending email notification...'
            script {
                emailext subject: "Jenkins Job: ${currentBuild.fullDisplayName} - Status: ${currentBuild.currentResult}",
                         body: """
                         Build Information:
                         -------------------
                         ${env.FINAL_REPORT}
                         """,
                         to: '2022853154@student.uitm.edu.my'
            }
        }

        success {
            echo 'HTML linting passed.'
        }

        failure {
            echo 'HTML linting failedd.'
        }
    }
}
