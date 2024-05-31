pipeline {
    agent {
        label 'ec2Slave'
    }
    
    stages {      
        stage('echo'){
            when {
                anyOf {
                    branch 'dev'
                    branch 'main'
                }
            }
            steps {
                script {
                    echo "executing from $BRANCH_NAME..."
                }
            }
        }

        
        stage('Checkout Code') {
            steps {
                // Checkout the specific GitHub repository
                 git branch: "$BRANCH_NAME", credentialsId: '71d7fab0-7e3a-4801-87fb-40aacc98bfa6', url: 'https://github.com/liwenbo55/TripTribe-Backend.git'
                sh "ls"
                sh """
                cat "hello.txt"
                """
            }
        }
            }
        }
