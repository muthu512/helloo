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
                        // Verify Node.js and npm versions
                        bat '"C:\\Program Files\\nodejs\\node.exe" -v'
                        bat '"C:\\Program Files\\nodejs\\npm.cmd" -v' // Use npm.cmd for Windows
                        
                        // Install dependencies
                        bat '"C:\\Program Files\\nodejs\\npm.cmd" install'
                    }
                }
            }
        }

        stage('Build React App') {
            steps {
                script {
                    def projectDir = "C:\\Users\\Dell-Lap\\Downloads\\react-helloworld-master\\react-helloworld-master"
                    
                    dir(projectDir) {
                        // Run the build command for the React application
                        bat '"C:\\Program Files\\nodejs\\npm.cmd" run build'
                        
                        // Verify build output
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

                    // Create the deployment directory if it doesn't exist
                    bat "if not exist \"${deployDir}\" mkdir \"${deployDir}\""

                    // Copy the built files to the deployment directory
                    bat "xcopy /S /I /Y \"${projectDir}\\build\\*\" \"${deployDir}\""
                    
                    // List the contents of the deployment directory to verify deployment
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
