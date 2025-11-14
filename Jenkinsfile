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
                script {
                    def targetDir = "/var/www/sample-ci-cd"
        
                    // cek apakah folder kosong
                    def isEmpty = sh(
                        script: "[ -z \"\$(ls -A ${targetDir} 2>/dev/null)\" ] && echo empty || echo notempty",
                        returnStdout: true
                    ).trim()
        
                    if (isEmpty == "empty") {
                        echo "Folder kosong → checkout scm"
        
                        dir(targetDir) {
                            checkout scm   // ini clone repo ke folder target
                        }
        
                    } else {
                        echo "Folder sudah ada → lakukan update (fetch + reset)"
        
                        sh """
                            cd ${targetDir}
                            git fetch --all
                            git reset --hard origin/main
                        """
                    }
                }
            }
        }
    }
}
