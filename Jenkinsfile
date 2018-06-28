#!groovy

class Constants {
    PackageArchiveName = 'Package'
}

class Utility {                       

    public static def emailBody() { 
        return """
          This is the email body
          And this as well
          and finally this!!!
        """
    }
    
    public static def getPackageScript(def packageName) {
        return """
            Compress-Archive -Path 'BuildOutput\\*' -DestinationPath 'BuildOutput\\${packageName}.zip'
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
        echo 'Generate documentation here...'
        bat script: """
            "C:\\Program Files\\doxygen\\bin\\doxygen"
        """
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'DoxygenOutput\\html', reportFiles: 'index.html', reportName: 'HTML Documentation', reportTitles: 'Documentation'])
      }
    }
    stage('Package') {
      steps {
        echo 'Perform packaging here...'
        powershell script: Utility.getPackageScript(Constants.PackageArchiveName)
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
                "pattern": "BuildOutput//${Constants.PackageArchiveName}.zip",
                "target": "generic-local//MyOrg//MyModule//MyModule-${env.BUILD_NUMBER_TIMESTAMP}.zip",
                "props": "MyProp1=MyProp1.Value;MyProp2=MyProp2.Value;MyProp3=MyProp3.Value"
              }
           ]
          }"""
          def buildInfo = Artifactory.newBuildInfo()
          buildInfo.number = "${env.BUILD_NUMBER_TIMESTAMP}"
          buildInfo.env.capture = true
          server.upload spec: uploadSpec, buildInfo: buildInfo
          server.publishBuildInfo buildInfo
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
