pipeline{

    agent any

    tools{
      maven 'Maven'
    }


    stages{

        stage("Cleanup"){
            steps{
                sh "rm -rf ./* .*"
            }
        }

        stage("Compile"){
          steps{
            sh "mvn compile"
          }
        }
    }


    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
