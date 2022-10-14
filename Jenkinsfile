pipeline {
    agent {
        node {
            label 'master'
            customWorkspace "D:\Projects"
        }
    } // End of Agent
    
    environment {
        ue4Path = "C:\\Unreal Engine\\UE_5.0"
        ue4Project = "MerchantLight"
        ueProjectFileName = "${ue4Project}.uproject"
        testSuiteToRun = "Game."//the '.' is used to run all tests inside the prettyname. The automation system searches for everything that has 'Game.' in it, so otherGame.'s tests would run too...
        testReportFolder = "TestsReport"
        testsLogName = "RunTests.log"
        pathToTestsLog = "${env.WORKSPACE}" + "\\Saved\\Logs\\" + "${testsLogName}"
        codeCoverageReportName="CodeCoverageReport.xml"
    } // End of Env
    
    
    stages {
        stage('Build') { 
            steps {
                echo "Building..."
                bat "BuildWithoutCooking.bat \"${ue4Path}\" \"${env.WORKSPACE}\" \"${ueProjectFilename}\""//builds our project
            }
            post {
                success { 
                    echo "Build Sucessful."
                }
                failure { 
                    echo "Build Failed."
                }
            }
        } // End of Build Stage
        stage('Test') { 
            steps {
                echo "Testing..."
                bat "TestRunnerAndCodeCoverage.bat \"${ue4Path}\" \"${env.WORKSPACE}\" \"${ueProjectFilename}\" \"${testSuiteToRun}\" \"${testReportFolder}\" \"${testsLogName}\" \"${codeCoverageReportName}\""//runs the tests
            }
            post {
                success { 
                    echo "Test Sucessful."
                }
                failure { 
                    echo "Test Failed."
                }
            }
        } // End of Test State
        stage('Deploy') { 
            steps {
                echo "Deploying..."
            }
        } // End of Deploy Stage
    } // End of Stages
} // End of Pipeline
