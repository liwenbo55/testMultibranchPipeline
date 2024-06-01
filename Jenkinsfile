pipeline {
    agent {
        label 'ec2Slave'
    }
    
    stages {      
        stage('echo'){
            when {
                anyOf {
                    branch 'dev'
                    branch 'master'
                }
            }
            steps {
                script {
                    echo "executing from $BRANCH_NAME..."
                }
            }
        }

        
        stage('Checkout Code') {
            when {
                anyOf {
                    branch 'dev'
                    branch 'master'
                }
            }
            steps {
                // Checkout the specific GitHub repository
                 // git branch: "$BRANCH_NAME", credentialsId: '71d7fab0-7e3a-4801-87fb-40aacc98bfa6', url: 'https://github.com/liwenbo55/testMultibranchPipeline.git'
                sh "ls"
                sh """
                cat "hello.txt"
                """
            }
        }

        stage('SonarQube'){
            when {
                anyOf {
                    branch 'dev'
                    branch 'master'
                }
            }
            steps {
                withSonarQubeEnv(installationName:'sonarCloud') {
                    sh'./mvnw cleanorg.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
                }
            }
        }
    }
}
