pipeline{
    agent any
    stages {
        stage("Unit tests"){
            steps{
                sh '''npm install && npm test'''
                step([$class: 'GitHubIssueNotifier',
                  issueAppend: true,
                  issueLabel: '',
                  issueTitle: '$JOB_NAME $BUILD_DISPLAY_NAME failed'])              
            }
        }
        stage("Code Quality Check up"){
            steps{
                sh '''/Users/Shared/Jenkins/Home/tools/hudson.plugins.sonar.SonarRunnerInstallation/Sonar_Scanner_-_3.2/bin/sonar-scanner \\
  -Dsonar.projectKey=Node-App\\
  -Dsonar.sources=. \\
  -Dsonar.host.url=http://localhost:9000 \\
  -Dsonar.login=70aaa33a26be4f808e70ef28382db29c18ecb942'''
            }
        }
    }
}
    
        
