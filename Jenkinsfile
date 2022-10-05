pipeline {
  agent {
    label 'android'
  }
  tools {
    jdk 'JDK8_Centos'
  }
  
  stages{
    stage('Checkout') {
      steps{
        echo "------------>Checkout<------------"
        checkout([
          $class: 'GitSCM', 
          branches: [[name: '*/staging']], 
          doGenerateSubmoduleConfigurations: false, 
          extensions: [], 
          gitTool: 'Default', 
          submoduleCfg: [], 
          userRemoteConfigs: [[
          credentialsId: 'GitHub_miguel.duran',
          url:'https://github.com/migueldur94/prueba_jenkins'
          ]]
          ])

      }
    }
    
   stage('Clean Build') {
      sh "pwd"
      sh 'ls -al'
      sh './gradlew clean'
    }
    
 post {
    always {
      echo 'This will always run'
    }
    success {
      echo 'This will run only if successful'
      junit allowEmptyResults: true, testResults: "${WORKSPACE}/test-results/*.xml"
    }
    failure {
      echo 'This will run only if failed'
//       mail (to: 'miguel.duran@ceiba.com.co',subject: "Failed Pipeline:${currentBuild.fullDisplayName}",body: "Something is wrong with ${env.BUILD_URL}")
    }
    unstable {
      echo 'This will run only if the run was marked as unstable'
    }
    changed {
      echo 'This will run only if the state of the Pipeline has changed'
      echo 'For example, if the Pipeline was previously failing but is now successful'
    }
  }
}
