pipeline {
  agent any
  environment {
    NEW_VERSION = '1.3.0'
    SERVER_CREDENTIALS = credentials('')
  }
  parameters{
    choice(name: 'VERSION', choices: ['1.1.0','1.2.0','1.3.0'], description: '')
    booleanParam(name: 'executeTests', defaultValue: true, description: '')
  }
  stages{
    stage("init"){
      steps {
        script {
          gv = load "script.groovy"
        }
      }
    }
    stage("build"){
      steps{
        script{
          gv.buildApp()
        }
      }
    }
    stage("test"){
      when{
        expression {
          params.executeTests == true
        }
      }
      steps{
        script{
          gv.testApp()
        }  
      }
    }
    stage("deploy"){
      steps{
        echo 'deploying the application'
        echo "deploying version ${params.VERSION}"
        script{
          gv.deployApp()
        }
      }
    }
  }
}
