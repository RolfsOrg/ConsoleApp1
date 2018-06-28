class Utility {                       

    public static def emailBody() { 
        return """
          This is the email body
          And this as well
          and finally this!!!
        """
    }
}

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
        bat script: """
          "C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Enterprise\\MSBuild\\15.0\\Bin\\MSBuild.exe" /t:Build /p:OutDir="BuildOutput"
         """
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
        echo '''Generate documentation here...
                and here
                and here as well!
        '''
      }
    }
    stage('Package') {
      steps {
        echo 'Perform packaging here...'
        powershell script:"""
          Compress-Archive -Path 'BuildOutput\\*' -DestinationPath 'BuildOutput\\Package.zip'
        """
      }
    }
    stage('Publish') {
      steps {
        echo 'Perform publishing here...'
        script {
          def server = Artifactory.server 'MyArtifactorySrv'
          def uploadSpec = """{
            "files": [
              {
                "pattern": "BuildOutput//Package.zip",
                "target": "generic-local//MyOrg//MyModule//MyModule-${env.BUILD_NUMBER_TIMESTAMP}.zip"
              }
           ]
          }"""
          server.upload(uploadSpec)
        }
      }
    }
  }
  post {
    always {
      echo 'Cleanup Workspace'
      // cleanWs()
      echo Utility.emailBody()
    }
  }
}
