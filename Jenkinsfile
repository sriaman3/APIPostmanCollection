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


        stage('Run API Test Cases in Parallel') {
              
                    steps {
                        bat 'docker run -v %CD%\\newman:/app/newman test11031992/bookingapi:1.0'
                    }
                
        }

        stage('Publish HTML Extra Reports') {
           
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: '*.html',
                            reportName: 'Booking API Report',
                            reportTitles: '',
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
