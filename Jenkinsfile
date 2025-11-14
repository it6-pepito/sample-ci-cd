pipeline {
    agent {
        label 'sample_linux_server'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application..."

                dir('/var/www/sample-ci-cd') {
                    checkout scm
                    sh '''
                    pwd
                    ls -l
                    '''
                }
            }
        }
    }
}
