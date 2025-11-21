pipeline{

    agent any

    tools{
      maven 'Maven'
    }


    stages{
        
        stage("Compile"){
          steps{
            sh "mvn compile"
          }
        }
    }


    post{
        always{
            sh "rm -rf ./* ./.*"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
