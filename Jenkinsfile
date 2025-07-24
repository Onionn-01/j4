pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning source code'
                git branch: 'master', url: 'https://github.com/Onionn-01/j4.git'
            }
        }
 
        stage('Publish') {
            steps {
                echo 'Copying workspace to C:\\myproject'
                // Nếu dùng Windows Agent thì dùng bat
                bat '''
                    xcopy "%WORKSPACE%" "C:\\myproject" /E /Y /I /R
                '''
            }
        }

        stage('Deploy to IIS') {
            steps {
                powershell '''
                    # Tạo website nếu chưa có
                    Import-Module WebAdministration
                    if (-not (Test-Path IIS:\\Sites\\MySite)) {
                        New-Website -Name "MySite" -Port 83 -PhysicalPath "C:\\myproject"
                    }
                '''
            }
        }
    }
}
