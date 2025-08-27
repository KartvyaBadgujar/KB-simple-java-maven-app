pipeline {
  agent {
    docker {
      image 'maven:3.9.9-eclipse-temurin-21'   // Maven + JDK 21
      args  '-v $HOME/.m2:/root/.m2'          // cache dependencies
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'java -version && mvn -v'          // sanity check
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Test') {
      when { expression { currentBuild.currentResult == null || currentBuild.currentResult == 'SUCCESS' } }
      steps {
        sh 'mvn -B test'
      }
    }
    stage('Deliver') {
      when { expression { currentBuild.currentResult == null || currentBuild.currentResult == 'SUCCESS' } }
      steps {
        sh 'echo "Deliver artifacts here"'
      }
    }
  }
}
