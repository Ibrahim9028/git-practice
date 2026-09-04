pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Code checked out from GitHub'
            }
        }

        stage('Test') {
            steps {
                sh '''
                    if [ -f jenkins-test.txt ]; then
                        echo "CI test passed"
                    else
                        echo "CI test failed"
                        exit 1
                    fi
                '''
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t devops-first-app:1.0 .'
            }
        }

        stage('Success') {
            steps {
                echo 'CI/CD pipeline completed successfully'
            }
        }
    }
}
