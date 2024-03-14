pipeline {
    agent any
    environment {
        FILE_PATH = 'C:\\jenkins\\workspace\\UIPath_Jenkins_Pipeline_main\\Bitbucket_Jenkins_UiPath_Package.1.0.14'
    }
    stages {
        stage('Checkout Git Repository') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/master']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [],
                    submoduleCfg: [],
                    userRemoteConfigs: [[credentialsId: 'myAccessKey', url: 'https://bitbucket.adesso-group.com/scm/~christian.adorf_adesso.de/notepad_automation.git']]
                ])
            }
        }
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
