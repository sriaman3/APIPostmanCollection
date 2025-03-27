pipeline {
    agent any
    stages {

        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage("Deploy to QA") {
            steps {
                echo "Deploying to QA"
            }
        }

        

        stage('Pull Docker Images') {
                stage('Pull Booking Image') {
                    steps {
                        bat 'docker pull test11031992/bookingapi:1.0'
                    }
                }
            
        }


        stage('Run API Test Cases in Parallel') {
              
                stage('Run Booking Tests') {
                    steps {
                        bat 'docker run --rm -v "%cd%\\newman:/app/results" test11031992/bookingapi:1.0'
                    }
                
            }
        }

        stage('Publish HTML Extra Reports') {
           
                stage('Publish Booking Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'booking.html',
                            reportName: 'Booking API Report',
                            reportTitles: ''
                        ])
                    }
                }
            }
        

        stage("Deploy to PROD") {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
