pipeline {
    agent any

    stages {

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

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f devops-first-app 2>/dev/null || true
                    docker run -d --name devops-first-app -p 8083:80 devops-first-app:1.0
                '''
            }
        }

        stage('Application Test') {
            steps {
                sh 'curl -f http://localhost:8083'
            }
        }

        stage('Success') {
            steps {
                echo 'CI/CD deployment completed successfully'
            }
        }
    }
}
