pipeline{
    agent any
    tools {nodejs "nodejs"}
    stages {
        stage("Unit tests"){
            steps{
                nodejs('nodejs') {
                        sh '''npm install && npm test'''
                }                          
            }
        }
        stage("Code Quality Check up"){
            environment {
                 scannerHome = tool 'SonarScanner'
            }
            steps{            
                 withSonarQubeEnv('SonarRapido'){
                 sh '''${scannerHome}/bin/sonar-scanner \\
                 -Dsonar.projectKey=Node-App\\
                 -Dsonar.sources=.'''
                 }
            }
        } 
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'minute') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    // Requires SonarQube Scanner for Jenkins 2.7+
                    waitForQualityGate abortPipeline: true
                }
            }
        }       
    }
}
