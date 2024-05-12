pipeline {
  agent any
  environment {
    NEW_VERSION = '1.3.0'
    SERVER_CREDENTIALS = credentials('')
  }
  tools {
    maven 'Maven'
    gradle
    jdk
  }
  parameters{
    choice(name: 'VERSION', choices: ['1.1.0','1.2.0','1.3.0'], description: '')
    booleanParam(name: 'executeTests', defaultValue: true, description: '')
  }
  stages{
    stage("build"){
      steps{
        echo 'building the application'
        echo "building version ${NEW_VERSION}"
      }
    }
    stage("test"){
      when{
        expression {
          params.executeTests == true
        }
      }
      steps{
        echo 'testing the application'
      }
    }
    stage("deploy"){
      steps{
        echo 'deploying the application'
        echo "deploying version ${params.VERSION}"
        withCredentials(
          [
            usernamePassword(credentials: '', usernameVariable: USER, passwordVariable: PWD)
          ]){
          
          }
      }
    }
  }
}