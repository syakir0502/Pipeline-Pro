pipeline {
    agent any

    environment {
        CHECKOUT_STATUS = 'Pending'
        BUILD_STATUS = 'Pending'
        TEST_STATUS = 'Pending'
        DEPLOYMENT_STATUS = 'Pending'
        DEPENDENCY_STATUS = 'Pending'
        LINT_STATUS = 'Pending'
        FINAL_REPORT = ''
    }

    tools {
        nodejs "NodeJS" // Ensure NodeJS is configured in Jenkins
    }

    options {
        // Ensures the pipeline runs all stages regardless of failures
        skipStagesAfterUnstable()
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                script {
                    // Simulate a failure
                    error('Simulated failure in Checkout Code')
                }
            }
            post {
                success {
                    script {
                        CHECKOUT_STATUS = 'Success'
                    }
                }
                failure {
                    script {
                        CHECKOUT_STATUS = 'Failed'
                    }
                }
                always {
                    echo "Checkout Status: ${CHECKOUT_STATUS}"
                }
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                script {
                    BUILD_STATUS = 'Success'
                }
            }
            post {
                success {
                    script {
                        BUILD_STATUS = 'Success'
                    }
                }
                failure {
                    script {
                        BUILD_STATUS = 'Failed'
                    }
                }
                always {
                    echo "Build Status: ${BUILD_STATUS}"
                }
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                script {
                    TEST_STATUS = 'Success'
                }
            }
            post {
                success {
                    script {
                        TEST_STATUS = 'Success'
                    }
                }
                failure {
                    script {
                        TEST_STATUS = 'Failed'
                    }
                }
                always {
                    echo "Test Status: ${TEST_STATUS}"
                }
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying application...'
                script {
                    DEPLOYMENT_STATUS = 'Success'
                }
            }
            post {
                success {
                    script {
                        DEPLOYMENT_STATUS = 'Success'
                    }
                }
                failure {
                    script {
                        DEPLOYMENT_STATUS = 'Failed'
                    }
                }
                always {
                    echo "Deployment Status: ${DEPLOYMENT_STATUS}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install --save-dev htmlhint'
                script {
                    DEPENDENCY_STATUS = 'Success'
                }
            }
            post {
                success {
                    script {
                        DEPENDENCY_STATUS = 'Success'
                    }
                }
                failure {
                    script {
                        DEPENDENCY_STATUS = 'Failed'
                    }
                }
                always {
                    echo "Dependency Status: ${DEPENDENCY_STATUS}"
                }
            }
        }

        stage('Lint HTML Files') {
            steps {
                echo 'Linting HTML files...'
                sh 'npx htmlhint "website/**/*.html"'
                script {
                    LINT_STATUS = 'Success'
                }
            }
            post {
                success {
                    script {
                        LINT_STATUS = 'Success'
                    }
                }
                failure {
                    script {
                        LINT_STATUS = 'Failed'
                    }
                }
                always {
                    echo "Lint Status: ${LINT_STATUS}"
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
            }

            echo "Final Report:\n${FINAL_REPORT}"

            // Ensure email gets sent
            emailext subject: "Jenkins Job: ${currentBuild.fullDisplayName} - Status: ${currentBuild.currentResult}",
                     body: "${FINAL_REPORT}",
                     to: '2022853154@student.uitm.edu.my'
        }
    }
}
