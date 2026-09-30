pipeline {
    agent any

    environment {
        APP_VERSION = '1.0.0'
        DEPLOY_ENVIRONMENT = 'production'
        APP_NAME = 'jenkins-pipeline-homework'
    }

    stages {

        stage('Checkout') {
            steps {
                script {
                    try {
                        echo "Starting checkout..."
                        checkout scm
                        echo "Checkout completed successfully."
                    } catch (Exception e) {
                        echo "Checkout failed: ${e.getMessage()}"
                        error("Checkout stage failed.")
                    }
                }
            }
        }

        stage('Build') {
            when {
                expression {
                    currentBuild.currentResult == 'SUCCESS'
                }
            }

            steps {
                script {
                    try {
                        echo "Building ${env.APP_NAME}"
                        echo "Application version: ${env.APP_VERSION}"

                        sh 'python3 --version'
                        sh 'python3 app.py'

                        echo "Build completed successfully."
                    } catch (Exception e) {
                        echo "Build failed: ${e.getMessage()}"
                        error("Build stage failed.")
                    }
                }
            }
        }

        stage('Test') {
            when {
                expression {
                    currentBuild.currentResult == 'SUCCESS'
                }
            }

            steps {
                script {
                    try {
                        echo 'Running tests...'

                        sh 'python3 -m venv .venv'
                        sh '.venv/bin/pip install -r requirements.txt'
                        sh 'PYTHONPATH=. .venv/bin/pytest -v'

                        echo 'Tests completed successfully.'
                    } catch (Exception e) {
                        echo "Tests failed: ${e.getMessage()}"
                        error 'Test stage failed.'
                    }
                }
            }
        }

        stage('Deploy') {
            when {
                expression {
                    env.DEPLOY_ENVIRONMENT == 'production' &&
                    currentBuild.currentResult == 'SUCCESS'
                }
            }

            steps {
                script {
                    try {
                        echo "Deploying ${env.APP_NAME}"
                        echo "Version: ${env.APP_VERSION}"
                        echo "Environment: ${env.DEPLOY_ENVIRONMENT}"

                        sh 'echo Deployment started'
                        sh 'echo Deployment completed successfully'

                    } catch (Exception e) {
                        echo "Deployment failed: ${e.getMessage()}"
                        error("Deploy stage failed.")
                    }
                }
            }
        }
    }

    post {
        success {
            echo "========================================"
            echo "PIPELINE SUCCESS"
            echo "Application: ${env.APP_NAME}"
            echo "Version: ${env.APP_VERSION}"
            echo "Environment: ${env.DEPLOY_ENVIRONMENT}"
            echo "========================================"
        }

        failure {
            echo "========================================"
            echo "PIPELINE FAILED"
            echo "Please check the Jenkins console output."
            echo "========================================"
        }

        always {
            echo "Pipeline execution finished."
            echo "Build number: ${env.BUILD_NUMBER}"
        }
    }
}