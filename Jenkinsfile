node ('master') {
  checkout scm
  stage ('Build') {
    withMaven(maven: 'M3') {
      if (isUnix()) {
        sh label: '', script: 'mvn -Dmaven.test.failure.ignore clean package'
        sh label: '', script: 'scp fitz@192.168.8.1:/media/card/elevate-run.txt .; cat elevate-run.txt.'
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
