pipeline {
  agent any
  stages {
    stage('Prepare') {
      steps {
        currentBuild.number = env.BUILD_NUMBER_TIMESTAMP
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
