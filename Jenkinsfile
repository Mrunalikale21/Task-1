pipeline {
    agent {
        docker { image 'openjdk:17' } // Use a containerized environment with Java
    }

    environment {
        APP_ENV = 'development'  // Change to 'production' to test production scenario
        VERSION = '1.0'
    }

    stages {
        stage('Environment Setup') {
            steps {
                script {
                    if (env.APP_ENV == 'production') {
                        echo "Production Build - Version: ${env.VERSION}"
                    } else {
                        echo "Development Build - Version: ${env.VERSION}"
                    }
                }
            }
        }

        stage('Parallel Execution') {
            parallel {
                stage('Compile Task 1') {
                    steps {
                        script {
                            sh 'javac HelloWorld1.java'
                        }
                    }
                }

                stage('Compile Task 2') {
                    steps {
                        script {
                            sh 'javac HelloWorld2.java'
                        }
                    }
                }
            }
        }

        stage('Store Build Outputs') {
            steps {
                archiveArtifacts artifacts: '*.class', fingerprint: true
            }
        }

        stage('Clean Up Workspace') {
            steps {
                cleanWs()
            }
        }
    }
}
