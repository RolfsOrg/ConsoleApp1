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
          currentBuild.description = "my new description" 
        }
      }
    }
    stage('Restore Packages') {
      steps {
        echo 'Restore packages here...'
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
}
