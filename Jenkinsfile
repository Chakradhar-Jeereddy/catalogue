pipeline{
    agent{
        node{
            label "agent"
        }
    }
    environment{
        appVersion = ""
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        booleanParam(name: 'Deploy', defaultValue: false, description: 'Do you want to deploy')

    }
    stages{
        stage('Read appVersion'){
            steps{
              def appVersion = readJSON file: 'package.json'
              echo "${appVersion.version}"
            }
        }
        stage('Build catalogue image'){
            steps{     
               docker build -t chakradhar05/catalogue:${appVersion.version} .
               docker images
            }
        }
        stage('Test'){
            steps{
              echo "Testing"
            }
        }
        stage('Deploy'){
            when{
                expression {params.deploy = "true"}
            }
            steps{
                 echo "Deploying"
            }
        }
    }
}