pipeline{
    agent any
    parameters{
        choice (name: 'DEPLO_ENV', choices:['int', 'stage', 'prod'], description: 'Target environment')
    }

    stages{
        stage('Build application'){
            agent any
            steps{
                sh 'mvn clean install'
            }     
           
               

        }
        stage('Deploy application'){
            agent any
            steps{
                sh 'mvn -v'
            }

        }
    }


}