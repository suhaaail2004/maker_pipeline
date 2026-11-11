pipeline {
    agent any

    environment {
        IMAGE_NAME   = 'maker-website'
        REGISTRY     = 'your-dockerhub-username'          // ← change me
        IMAGE_TAG    = "${env.BUILD_NUMBER}"
        DOCKER_CREDS = 'docker-credentials-id'            // ← Jenkins credential ID
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Passed...'
            }
        }

        stage('Build and Test') {
            steps {
                echo 'Building project...'
                // Add your build command here, e.g: sh 'npm install'
                echo 'Running tests...'
                // Add your test command here, e.g: sh 'npm test'
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_CREDS}") {
                        def img = docker.build("${REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}")
                        img.push()
                        img.push('latest')
                    }
                }
            }
        }

        stage('Update Deployment File') {
            steps {
                sh """
                    sed -i 's|IMAGE_PLACEHOLDER|${REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}|g' manifests/deployment.yaml
                    cat manifests/deployment.yaml
                """
            }
        }

    }

    post {
        success { echo "✅ Pipeline succeeded — image: ${REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}" }
        failure { echo "❌ Pipeline failed." }
    }
}
