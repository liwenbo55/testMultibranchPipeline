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
        stage('SonarQube Analysis') {

            steps {
                script {
                    scannerHome = tool "SONARSCANNER"
                }
                withSonarQubeEnv('sonarCloud') {
                   // sh '''
                   // ${scannerHome}/bin/sonar-scanner \
                   //            -Dsonar.organization=liwenbo55 \
                   //            -Dsonar.projectKey=testtest1 \
                   //            -Dsonar.sources=. \
                   //            -Dsonar.host.url=https://sonarcloud.io
                   // '''
                  // sh "${scannerHome}/bin/sonar-scanner -Dsonar.organization=liwenbo55 -Dsonar.projectKey=testtest1 -Dsonar.sources=. -Dsonar.host.url=https://sonarcloud.io"
                   sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=triptribe-frontend \
                   -Dsonar.projectName=triptribe-frontend \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=. '''
                }
              }
            
            // environment {
            //     scannerHome = tool "SONARSCANNER"
            // }
            // steps {
            //    withSonarQubeEnv("sonarCloud") {
                   // sh '''
                   // ${scannerHome}/bin/sonar-scanner \
                   //            -Dsonar.organization=liwenbo55 \
                   //            -Dsonar.projectKey=testtest1 \
                   //            -Dsonar.sources=. \
                   //            -Dsonar.host.url=https://sonarcloud.io
                   // '''
            //     }
            // }    
        }
        // stage('SonarQube'){
        //     when {
        //         anyOf {
        //             branch 'dev'
        //             branch 'master'
        //         }
        //     }
        //     steps {
        //         // withSonarQubeEnv(installationName:'sonarCloud') {
        //         //     sh """
        //         //     sonar-scanner \
        //         //       -Dsonar.organization=liwenbo55 \
        //         //       -Dsonar.sources=. \
        //         //       -Dsonar.projectKey= liwenbo55_testMultibranchPipeline \
        //         //       """
        //         // }
        //         withSonarQubeEnv("${SONARSERVER}") {                    
        //             sh '''${scannerHome}/bin/sonar-scanner 
        //             -Dsonar.projectKey=triptribe-frontend \                    
        //             -Dsonar.projectName=triptribe-frontend \                    
        //             -Dsonar.projectVersion=1.0 \                    
        //             -Dsonar.sources=src/'''                 }
        //     }
        // }
    }
}
