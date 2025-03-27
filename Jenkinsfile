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
                
                    steps {
                        bat 'docker pull test11031992/bookingapi:1.0'
                    }
            
        }


        stage('Run API Test Cases in Parallel') {
              
                    steps {
                        bat 'docker run --rm -v "%cd%\\newman:/app/results" test11031992/bookingapi:1.0'
                    }
                
        }

        stage('Publish HTML Extra Reports') {
           
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'booking.html',
                            reportName: 'Booking API Report',
                            reportTitles: '',
                            useWrapperFileDirectly: true
                        ])
                    }
                
            }
        

        stage("Deploy to PROD") {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
