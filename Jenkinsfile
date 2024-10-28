pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git credentialsId: 'muthu512', url: 'https://github.com/muthu512/helloo.git', branch: 'master'
            }
        }

        stage('Check Environment Variables') {
            steps {
                script {
                    bat 'echo %PATH%'  // Print the PATH variable to verify environment
                }
            }
        }

        stage('Check for package.json') {
            steps {
                script {
                    def projectDir = "C:\\Users\\Dell-Lap\\Downloads\\react-helloworld-master\\react-helloworld-master"
                    
                    // Check for the existence of package.json
                    dir(projectDir) {
                        bat 'if exist "package.json" (echo package.json exists) else (echo package.json not found && exit 1)'
                    }
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    def projectDir = "C:\\Users\\Dell-Lap\\Downloads\\react-helloworld-master\\react-helloworld-master"
                    
                    dir(projectDir) {
                        bat '"C:\\Program Files\\nodejs\\node.exe" -v'
                        bat '"C:\\Program Files\\nodejs\\npm.cmd" -v'
                        
                        // Attempt to install dependencies and handle errors gracefully
                        bat '''
                        call "C:\\Program Files\\nodejs\\npm.cmd" install --legacy-peer-deps || (
                            echo Failed to install some dependencies. Trying again without the problematic package...
                            call "C:\\Program Files\\nodejs\\npm.cmd" install --no-package-lock --legacy-peer-deps
                        )
                        || exit 1
                        '''
                    }
                }
            }
        }

        stage('Build React App') {
            steps {
                script {
                    def projectDir = "C:\\Users\\Dell-Lap\\Downloads\\react-helloworld-master\\react-helloworld-master"
                    
                    dir(projectDir) {
                        bat '"C:\\Program Files\\nodejs\\npm.cmd" run build'
                        bat 'dir build'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def deployDir = "C:\\Users\\Dell-Lap\\Downloads\\node\\"
                    def projectDir = "C:\\Users\\Dell-Lap\\Downloads\\react-helloworld-master\\react-helloworld-master"

                    bat "if not exist \"${deployDir}\" mkdir \"${deployDir}\""
                    bat "xcopy /S /I /Y \"${projectDir}\\build\\*\" \"${deployDir}\""
                    bat "dir \"${deployDir}\""
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
