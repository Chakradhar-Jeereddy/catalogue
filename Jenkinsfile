pipeline{
  agent{
    node{
      label "AGENT"
    }
  }
  environment{
    course = "jenkins"
  }
  options{
    disableConcurrentBuilds()
  }
  parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'Deploy', defaultValue: false, description: 'Do you want to deploy?')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
  }
  stages{
    stage('Build'){
      steps{
        script{
          sh"""
           echo "hello"
          """
        }
      }
    }
    stage('Test'){
      steps{
          sh"""
          echo $course
          """
      }
    }
    stage('Deploy'){
      when{
        expression { "${params.Deploy}" == "true" }
      }
      steps{
        script{
          sh"""
          echo "scripted build"
          """
        }
      }
    }
  }
  post{
    always{
      echo "always say hi"
      cleanWs()
    }
    success{
      echo "say the build successful"
    }
    failure{
      echo "say the build failed"
    }
    aborted{
      echo "timeout exceeded"
    }
  }
}
