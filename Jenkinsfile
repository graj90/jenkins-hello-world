pipeline {
    agent any

    tools {
        maven "maven399"  // Ensure this matches the name set in Global Tool Configuration
    }

    stages {
        stage("Echo Version") {
            steps {
                sh "echo 'Printing Maven version...'"
                sh "mvn -version"
            }
        }

        stage("Build") {
            steps {
                sh "mvn clean package -DskipTests=true"
            }
        }

        stage("Unit Test") {
            steps {
                script {
                    try {
                        sh "mvn test"
                    } catch (Exception e) {
                        echo "Tests failed: ${e}"
                        currentBuild.result = 'UNSTABLE'  // Mark as unstable instead of failure
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Build Completed."
        }
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
