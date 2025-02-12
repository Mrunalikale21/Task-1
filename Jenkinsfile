pipeline {
    agent any  // Runs on any available agent

    environment {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-17"   // Set Java home path
        PATH = "${JAVA_HOME}\\bin;${env.PATH}"  // Append Java bin directory to PATH
    }

    stages {
        stage('Setup Environment') {
            steps {
                script {
                    if (env.BUILD_ENV == 'production') {
                        echo "Running in PRODUCTION environment"
                    } else {
                        echo "Running in DEVELOPMENT environment"
                    }
                }
            }
        }

        stage('Parallel Execution') {
            parallel {
                stage('Task 1 - Compile Java Program 1') {
                    steps {
                        script {
                            writeFile file: 'Task1.java', text: '''
                                public class Task1 {
                                    public static void main(String[] args) {
                                        System.out.println("Hello Jenkins from Task 1.");
                                    }
                                }
                            '''
                            bat 'javac Task1.java'
                        }
                    }
                }
                stage('Task 2 - Compile Java Program 2') {
                    steps {
                        script {
                            writeFile file: 'Task2.java', text: '''
                                public class Task2 {
                                    public static void main(String[] args) {
                                        System.out.println("Hello Jenkins from Task 2.");
                                    }
                                }
                            '''
                            bat 'javac Task2.java'
                        }
                    }
                }
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                archiveArtifacts artifacts: '*.class', fingerprint: true
                echo "Artifacts archived successfully."
            }
        }

        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                echo "Workspace cleaned successfully."
            }
        }
    }

    post {
        success {
            echo "Pipeline execution completed successfully."
        }
        failure {
            echo "Pipeline execution failed."
        }
    }
}
