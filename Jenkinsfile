node ('master') {
  checkout scm
  stage ('Build') {
    withMaven(maven: 'M3') {
      if (isUnix()) {
        sh label: '', script: 'mvn -Dmaven.test.failure.ignore clean package'
        sh label: '', script: 'ssh fitz@192.168.8.1 "cat /media/card/elevate-run.txt"'
      } else {
        bat label: '', script: 'mvn -Dmaven.test.failure.ignore clean package'
      }
    }
  }
  stage ('Results') {
    junit '**/target/surefire-reports/TEST-*.xml'
    archiveArtifacts 'target/*.jar'
  }
}
