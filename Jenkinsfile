pipeline {
    agent any

    environment {
        BUILD_START_TIME = ''
        BUILD_END_TIME = ''
        BUILD_DURATION = ''
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                // Simulate code checkout (You can actually use git checkout in real scenarios)
                sh 'echo "Simulating Git checkout..."'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                // Simulate installing dependencies (e.g., npm install, pip install)
                sh 'echo "Simulating dependency installation..."'
                sleep 3 // Simulate a delay
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                // Simulate running tests (e.g., npm test, pytest)
                sh 'echo "Simulating test execution..."'
                sleep 5 // Simulate test execution
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                // Simulate build process (e.g., npm build, mvn package)
                sh 'echo "Simulating application build..."'
                sleep 4 // Simulate build process
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying application to staging...'
                // Simulate deployment process (e.g., kubectl apply, ssh into server)
                sh 'echo "Simulating deployment..."'
                sleep 3 // Simulate deployment time
            }
        }

        stage('Post-Deployment Checks') {
            steps {
                echo 'Performing post-deployment checks...'
                // Simulate post-deployment checks (e.g., health check, system verification)
                sh 'echo "Simulating post-deployment checks..."'
                sleep 2 // Simulate checks
            }
        }
    }

    post {
        always {
            script {
                // Capture start and end times with formatted output
                def startTime = new Date()
                BUILD_START_TIME = startTime.format("yyyy-MM-dd HH:mm:ss")
                
                def endTime = new Date()
                BUILD_END_TIME = endTime.format("yyyy-MM-dd HH:mm:ss")
                
                BUILD_DURATION = (endTime.time - startTime.time) / 1000

                // Send email with build information
                try {
                    emailext(
                        to: '2022853154@student.uitm.edu.my',
                        subject: "Jenkins Build Status: ${currentBuild.currentResult}",
                        body: """
                        <h2>The Jenkins build has completed.</h2>
                        <br/>
                        <b>Build Details:</b>
                        <pre>
                        =====================
                        Build Status: ${currentBuild.currentResult}
                        Build Start Time: ${BUILD_START_TIME}
                        Build End Time: ${BUILD_END_TIME}
                        Build Duration: ${BUILD_DURATION} seconds

                        Console Output:
                        <a href="${BUILD_URL}console">${BUILD_URL}console</a>
                        </pre>
                        """,
                        mimeType: 'text/html'
                    )
                } catch (Exception e) {
                    echo "Error sending email: ${e.message}"
                }
            }
        }
    }
}
