pipeline {
  //configuration...
  agent {
    node {
      label 'master'
      customWorkspace "D:/Projects/MerchantLight"
    }
  }
  
   environment {
    ue4Path = "C:\\Program Files\\Epic Games\\UE_4.22  C:\\Unreal Engine\\UE_5.0"
    ue4Project = "MerchantLight"
    ueProjectFileName = "${ue4Project}.uproject"
    testSuiteToRun = "Game."//the '.' is used to run all tests inside the prettyname. The automation system searches for everything that has 'Game.' in it, so otherGame.'s tests would run too...
    testReportFolder = "TestsReport"
    testsLogName = "RunTests.log"
    pathToTestsLog = "${env.WORKSPACE}" + "\\Saved\\Logs\\" + "${testsLogName}"
    codeCoverageReportName="CodeCoverageReport.xml"
  }


//pipeline execution
  stages {//the pipeline stages

    stage('Building') {//a pipeline stage called 'Building'

      steps {//steps made in the 'Building' stage

        echo 'Build Stage Started.'//a step in the stage
        bat "BuildWithoutCooking.bat \"${ue4Path}\" \"${env.WORKSPACE}\" \"${ueProjectFilename}\""//builds our project
      }//end of the 'building' steps

      post {//actions made after the stage execution
        
       //things that will be done always, after the stage execution...

        success {//things that will be done only if the stage execution succeeds:
          echo 'Build Stage Successful.'
        }
        failure {//things that will be done only if the stage fails:
          echo 'Build Stage Unsuccessful.'
        }
      }
    }

    stage('Testing') {
      steps {
        echo 'Testing Stage Started.'
        bat "TestRunnerAndCodeCoverage.bat \"${ue4Path}\" \"${env.WORKSPACE}\" \"${ueProjectFilename}\" \"${testSuiteToRun}\" \"${testReportFolder}\" \"${testsLogName}\" \"${codeCoverageReportName}\""//runs the tests
      }
      post {
        success {
          echo 'Testing Stage Successful.'
        }
        failure {
          echo 'Testing Stage Unsuccessful.'
        }
      }
    }
  //end of stages
  }
  
  post {
    always{
      echo 'Tests finished, printing log.'
      bat "type ${pathToTestsLog}"
      echo 'Formatting TestsReport from JSon to JUnit XML'
      formatUnitTests()

      echo "Publish Code Coverage Report."
      cobertura(coberturaReportFile:"${codeCoverageReportName}")
      
      echo 'Cleaning up workspace:'
      echo '-checking current workspace.'
      powershell label: 'show workspace', script: 'dir $WORKSPACE'
      bat 'git reset --hard'//resets to HEAD, to the commit in the cloned repository.
      bat 'git clean -dffx .'//removes untracked files.
      echo '-checking clean workspace.'
      powershell label: 'show workspace', script: 'dir $WORKSPACE'
  }
  
//end of pipeline
}
