pipeline {
    agent any

    environment {
        BUILD_VERSION = '1.0.0'
        STAGE_SUMMARY = ''
    }

    tools {
        nodejs "NodeJS" // Ensure NodeJS is configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                script {
                    currentBuild.description = "Checkout: Success"
                }
            }
            post {
                success {
                    script {
                        currentBuild.description = "Checkout Code: Success"
                        STAGE_SUMMARY += '- Checkout Code: Success\n'
                    }
                }
                failure {
                    script {
                        currentBuild.description = "Checkout Code: Failed"
                        STAGE_SUMMARY += '- Checkout Code: Failed\n'
                    }
                }
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                script {
                    error('Simulating Build Failure') // Intentional failure
                }
            }
            post {
                success {
                    script {
                        STAGE_SUMMARY += '- Build Application: Success\n'
                    }
                }
                failure {
                    script {
                        STAGE_SUMMARY += '- Build Application: Failed\n'
                    }
                }
            }
        }

        stage('Run Tests') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                echo 'Running tests...'
                script {
                    STAGE_SUMMARY += """
                    - Run Tests: Success
                        Total Tests: 20
                        Passed: 18
                        Failed: 2
                    """
                }
            }
            post {
                success {
                    script {
                        STAGE_SUMMARY += '- Run Tests: Success\n'
                    }
                }
                failure {
                    script {
                        STAGE_SUMMARY += '- Run Tests: Failed\n'
                    }
                }
            }
        }

        stage('Deploy Application') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                echo 'Deploying application...'
                script {
                    STAGE_SUMMARY += '- Deploy Application: Success\n'
                }
            }
            post {
                success {
                    script {
                        STAGE_SUMMARY += '- Deploy Application: Success\n'
                    }
                }
                failure {
                    script {
                        STAGE_SUMMARY += '- Deploy Application: Failed\n'
                    }
                }
            }
        }

        stage('Lint HTML Files') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                echo 'Linting HTML files...'
                script {
                    sh 'npx htmlhint "website/**/*.html"' // Simulating success
                }
            }
            post {
                success {
                    script {
                        STAGE_SUMMARY += '- Lint HTML Files: Success\n'
                    }
                }
                failure {
                    script {
                        STAGE_SUMMARY += '- Lint HTML Files: Failed\n'
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                def emailBody = """
                Jenkins Job: ${currentBuild.fullDisplayName}
                Status: ${currentBuild.currentResult}

                Stage Status Summary:
                ----------------------
                ${STAGE_SUMMARY}
                """
                echo "Email Body:\n${emailBody}"

                // Send email
                emailext subject: "Jenkins Job: ${currentBuild.fullDisplayName} - Status: ${currentBuild.currentResult}",
                         body: emailBody,
                         to: '2022853154@student.uitm.edu.my'
            }
        }

        success {
            echo 'Pipeline completed successfully.'
        }

        failure {
            echo 'Pipeline encountered errors.'
        }
    }
}
