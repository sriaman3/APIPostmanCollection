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
            parallel {
                stage('Pull GoRest Image') {
                    steps {
                       bat 'docker pull test11031992/bookingapi:1.0'
                    }
                }
                stage('Pull Booking Image') {
                    steps {
                        bat 'docker pull test11031992/bookingapi:1.0'
                    }
                }
            }
        }

        stage('Prepare Newman Results Directory') {
            steps {
                bat '''
                    if exist 'mkdir "%cd%\\newman"' (
                    rmdir /s /q 'mkdir "%cd%\\newman"'
                    )
                    mkdir "%cd%\\newman"
                    '''
            }
        }

        stage('Run API Test Cases in Parallel') {
            parallel {
                stage('Run GoRest Tests') {
                    steps {
                         bat 'docker run --rm -v "%cd%\\newman:/app/results" test11031992/bookingapi:1.0'
                    }
                }
                stage('Run Booking Tests') {
                    steps {
                        bat 'docker run --rm -v "%cd%\\newman:/app/results" test11031992/bookingapi:1.0'
                    }
                }
            }
        }

        stage('Publish HTML Extra Reports') {
            parallel {
                stage('Publish GoRest Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'gorest.html',
                            reportName: 'GoRest API Report',
                            reportTitles: ''
                        ])
                    }
                }
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
        }

        stage("Deploy to PROD") {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
