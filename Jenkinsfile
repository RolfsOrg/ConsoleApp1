pipeline {
  agent any
  
  options {
    disableConcurrentBuilds()
  }
  
  stages {
    stage('Prepare') {
      steps {
        echo 'Prepare here...'
        script {
          currentBuild.displayName = env.BUILD_NUMBER_TIMESTAMP
        }
      }
    }
    stage('Restore Packages') {
      steps {
        bat script: 'C:\\Rolf\\Tools\\NuGet\\nuget.exe restore'
      }
    }
    stage('Build') {
      steps {
        echo 'Perform build here...'
      }
    }
    stage('Run Tests') {
      steps {
        echo 'Perform testing here...'
      }
    }
    stage('Inspect') {
      steps {
        echo 'Perform inspection here...'
      }
    }
    stage('Generate Documentation') {
      steps {
        echo 'Generate documentation here...'
      }
    }
    stage('Package') {
      steps {
        echo 'Perform packaging here...'
      }
    }
    stage('Publish') {
      steps {
        echo 'Perform publishing here...'
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}
