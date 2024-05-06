pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('doc') {
      steps {
        sh 'mvn javadoc:jar'
      }
    }
    stage('pmd') {
      steps {
        sh 'mvn pmd:pmd'
      }
    }
    stage('Test Report') {
      steps {
        sh 'mvn test --fail-never'
        sh 'mvn surefire-report:report'
      }
    }

    
  }
  post {
      always {
          archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
          archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
          archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
      }
  }  
  
}
