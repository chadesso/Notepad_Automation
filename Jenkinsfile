pipeline {
    agent any
    environment {
        FILE_PATH = 'C:\\jenkins\\workspace\\UIPath_main\\Jenkins_Library_2.1.0.13.nupkg'
    }
    stages {
        stage('Upload Package') {
            steps {
                // Use withCredentials to safely handle the authToken
                withCredentials([string(credentialsId: 'authToken', variable: 'AUTH_TOKEN')]) {
                    // Use bat step for Windows command execution
                    bat """
                        curl -X POST ^
                          https://cloud.uipath.com/adesso_se/adessoSE/odata/Processes/UiPath.Server.Configuration.OData.UploadPackage ^
                          -H "Authorization: Bearer %AUTH_TOKEN%" ^
                          -H "Content-Type: multipart/form-data" ^
                          -H "Accept: application/json" ^
                          -F "file=@${env.FILE_PATH}"
                    """
                }
            }
        }
    }
}