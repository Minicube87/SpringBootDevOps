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
            echo "================"
        }
        success{
            cleanWs()
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
