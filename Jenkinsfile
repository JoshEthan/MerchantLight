pipeline {
    agent {
        node {
            label 'master'
            customWorkspace "D:/Projects"
        }
    }
    
    environment {
        ue4Path = "C:\\Unreal Engine\\UE_5.0"
        ue4Project = "MerchantLight"
        ueProjectFileName = "${ue4Project}.uproject"
        testSuiteToRun = "Game."//the '.' is used to run all tests inside the prettyname. The automation system searches for everything that has 'Game.' in it, so otherGame.'s tests would run too...
        testReportFolder = "TestsReport"
        testsLogName = "RunTests.log"
        pathToTestsLog = "${env.WORKSPACE}" + "\\Saved\\Logs\\" + "${testsLogName}"
        codeCoverageReportName="CodeCoverageReport.xml"
    }
    
    
    stages {
        stage('Build') { 
            steps {
                echo "Building..."
            }
        }
        stage('Test') { 
            steps {
                echo "Testing..." 
            }
        }
        stage('Deploy') { 
            steps {
                echo "Deploying..."
            }
        }
    }
}
