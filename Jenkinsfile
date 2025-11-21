pipeline{

    agent any

    tools{
      maven 'Maven'
    }

    environment{
        creds=credentials('nexus_kurs3')
        url='https://nexus.skyered-devops.de/repository/Kurs3-Raw'
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

        stage("Upload"){
          steps{
            sh"""
            DEP_FILE=dependency-tree.txt
            WAR_FILE=$(ls target/*.war)

            'curl -u "$creds_USR:$creds_PSW" --upload-file "$DEP_FILE" "$url/$DEP_FILE" '
            'curl -u "$creds_USR:$creds_PSW" --upload-file "$WAR_FILE" "$url/$WAR_FILE" '
            """
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
