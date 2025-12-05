pipeline {
  agent any

  tools {
    // name here must match the name of the configured Maven installation in Jenkins -> Global Tool Configuration
    maven 'Maven' 
    jdk 'JDK17' 
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }

    stage('Run') {
      steps {
        // show program output
        sh 'java -cp target/myfirstapp-1.0-SNAPSHOT.jar com.mycompany.app.App'
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      junit 'target/surefire-reports/*.xml' // safe even if there are no tests
    }
  }
}
