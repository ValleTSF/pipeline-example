pipeline{
    agent any
    parameters{
        choice (name: 'DEPLOY_ENV', choices:['int', 'stage', 'prod'], description: 'Target environment')
    }

    stages{
        stage('Build application'){
            agent any
            steps{
                sh 'mvn clean install'
            }     
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    publishHTML([allowMissing: false,
                        alwaysLinkToLastBuild: false, 
                        keepAll: false, 
                        reportDir: 'target/surefire-reports/', 
                        reportFiles: 'index.html', 
                        reportName: 'Unit tests', 
                        reportTitles: 'Unit tests'])
                        
                        
                    publishHTML([allowMissing: false,
                        alwaysLinkToLastBuild: false, 
                        keepAll: false, 
                        reportDir: 'target/site/jacoco/', 
                        reportFiles: 'index.html', 
                        reportName: 'Test Coverage', 
                        reportTitles: 'Test Coverage'])
                }
                
                success{
                    archive 'target/calc-jsf-1.0.war'
                }
            }
              
        }
        stage('Deploy application'){
            agent any
            steps{
                sh 'asadmin --port 4848 deploy --force --name calc-${DEPLOY_ENV} --contextroot calc-${DEPLOY_ENV} target/calc-jsf-1.0.war'
            }

        }
    }


}