pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git credentialsId: 'muthu512', url: 'https://github.com/muthu512/html.git', branch: 'master'
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
                    // Set the project directory where package.json is located
                    def projectDir = "C:\\Users\\Dell-Lap\\Downloads\\react-hello-world-master\\react-hello-world-master"
                    
                    // Navigate to the project directory and check for package.json
                    dir(projectDir) {
                        bat 'if exist "package.json" (echo package.json exists) else (echo package.json not found && exit 1)'
                    }
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Set the project directory where package.json is located
                    def projectDir = "C:\\Users\\Dell-Lap\\Downloads\\react-hello-world-master\\react-hello-world-master"
                    
                    // Navigate to the project directory for installation
                    dir(projectDir) {
                        // Check Node.js and npm versions to ensure they're installed
                        bat '"C:\\Program Files\\nodejs\\node" -v'
                        bat '"C:\\Program Files\\nodejs\\npm" -v'
                        
                        // Install dependencies using npm install
                        bat '"C:\\Program Files\\nodejs\\npm" install || exit 1'
                    }
                }
            }
        }

        stage('Build React App') {
            steps {
                script {
                    // Set the project directory where package.json is located
                    def projectDir = "C:\\Users\\Dell-Lap\\Downloads\\react-hello-world-master\\react-hello-world-master"
                    
                    // Navigate to the project directory for building
                    dir(projectDir) {
                        // Run the build command for the React application
                        bat '"C:\\Program Files\\nodejs\\npm" run build || exit 1'
                        // List the contents of the build directory to verify the build output
                        bat 'dir build'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Create the deployment directory if it doesn't exist
                    bat 'if not exist "C:\\Users\\Dell-Lap\\Downloads\\node\\" mkdir "C:\\Users\\Dell-Lap\\Downloads\\node\\"'
                    // Copy the built files to the deployment directory
                    bat 'xcopy /S /I /Y "C:\\Users\\Dell-Lap\\Downloads\\react-hello-world-master\\react-hello-world-master\\build\\*" "C:\\Users\\Dell-Lap\\Downloads\\node\\"'
                    // List the contents of the deployment directory to verify deployment
                    bat 'dir "C:\\Users\\Dell-Lap\\Downloads\\node\\"'
                }
            }
        }
    }
}
