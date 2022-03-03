pipeline {
    agent any 
    tools {
      maven 'Maven'
    }
    environment {
      NEW_VERSION = '1.3.0'
      SERVER_CREDENTIALS = credentials('github-credentials')
    }
  
    parameters {
      string(name: 'VERSION', defaultValue: 'version to deploy on pod')
      choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
      booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
  
    stages {
        stage('build') {
            steps {
                echo 'building the application' 
                echo "building version ${NEW_VERSION}"
            }
        }
        stage('test') {
            when {
              expression{
                params.executeTests == true
              }
            }
            steps {
                echo 'testing the application' 
            }
        }
        stage('deploy') {
              steps {
                echo "deploying the application version ${params.VERSION}"
                  withCredentials([
                    usernamePassword(credentials: 'github-credentials',
                                    usernameVariable: USER,
                                    passwordVariable: PWD)
                  ]) {
                    sh "some script ${USER} ${PWD}"
                  }
              }
        }
    }
}
