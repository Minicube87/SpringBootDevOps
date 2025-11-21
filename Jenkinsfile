pipeline{

    agent any

    tools{
      maven 'Maven'
    }

    parameters {
    choice(name: 'ENVIRONMENT', choices: ['dev', 'prod', 'test'], description: 'Environment-Auswahl')
    choice(name: 'SKIP_TESTS', choices: ['true', 'false'], description: 'Tests überspringen?')
    }


    stages{

        stage("Compile"){
          steps{
            sh "mvn compile"
          }
        }
        
        stage("Build"){
          steps{
            sh "mvn clean package -P${params.ENVIRONMENT} -DskipTests=${params.SKIP_TESTS}"
          }
        }

        stage("Dependencies"){
          steps{
            sh "mvn dependency:tree"
          }
        }

        stage("Create file Dependency Tree"){
          steps{
            sh "mvn dependency:tree -DoutputFile=dependency-tree.txt -DoutputType=text"
          }
        }
    }


    post{
        always{
            echo "================"
        }
        success{
            echo "sucess" //cleanWs()
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
