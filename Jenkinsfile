pipeline{
    agent any
    // tools{
        // nodejs 'NodeJS'
    // } 
    environment {
        SONAR_PROJECT_KEY = 'nodsjs_cici_pipeline'
        SONAR_SCANNER_HOME = tools 'SonarQubeScanner'
            
    }

    stages{
        stage ('clone code'){
            steps{
                git branch: 'main', credentialsId: 'Git-token_personal_account', url: 'https://github.com/DeepDN/Nodejs-CICD-pipeline.git'
            }
        }
        stage ('unit test'){
            steps{  
                sh 'npm test'
                sh 'npm install'
            }
        }
         stage ('Sonarqube scanner'){
            steps{
                withCredentials([string(credentialsId: 'SONARQUBE_TOKEN', variable: 'SONAR_TOKEN')]) {
                    withSonarQubeEnv('sonarqube') {
                        sh '''
                        ${SONAR_SCANNER_HOME}/bin/sonar-scanner \
                        -Dsonar.projectKeys=${SONAR_PROJECT_KEY} \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://http://localhost:9000 \
                        -Dsonar.login=${SONAR_TOKEN}
                        '''

                    }
                }
            }
        }
    }
}