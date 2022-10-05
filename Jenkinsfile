def err = null
try {
  
    node {
        stage('Dependencies') {
          sh 'export JAVA_HOME=/opt/jdk1.8.0_201'
          sh 'export JRE_HOME=/opt/jdk1.8.0_201/jre'
          sh 'export PATH=$PATH:/opt/jdk1.8.0_201/bin:/opt/jdk1.8.0_201/jre/bin'
          sh 'echo $JAVA_HOME'
        }
        
        stage('Clean Build') {
          sh "pwd"
          sh 'ls -al'
          sh './gradlew clean'
        }
        
        stage('Build release ') {
            sh './gradlew assembleRelease'
        }
      
        stage('Compile') {
            archiveArtifacts artifacts: '**/*.apk', fingerprint: true, onlyIfSuccessful: true            
        }
    }
  
} catch (caughtError) { 
    
    err = caughtError
    currentBuild.result = "FAILURE"

} finally {
    
    if(currentBuild.result == "FAILURE"){
              sh "echo 'Build FAILURE'"
    }else{
         sh "echo 'Build SUCCESSFUL'"
    }
   
}
