pipeline {
    agent any

    stages {

        // stage 1
        stage('setup environment') {
            steps {
                echo "installing dependencies"
                bat'''
                    pip install --upgrade pip
                    pip install pytest pytest-cov pytest-html
                '''
            }
        }

        stage('Run tests') {
            steps{
                echo "running tests and generating reporst"
                bat '''
                    pytest --junitxml=report.xml --cov=calculator --cov-report=html --html=report.html
                    '''
            }
        }

        stage('publish junit test report') {
            steps {
                echo "publishing junit test report"
                junit 'report.xml'
            }
        }

        stage('publish HTML coverage report') {
            steps{
                echo "publishing HTML coverage report"
                publishHTML(target: [
                    reportDir: 'htmlcov',
                    reportFiles: 'index.html',
                    reportName: 'HTML Coverage',
                ])
            }
        }

        stage('publish html test reports') {
            steps{
                echo "publishing html test reports"
                publishHTML(target: [
                    reportDir: '.',
                    reportFiles: 'report.html',
                    reportName: 'Test Report',
                ])
            }
        }
    }
}