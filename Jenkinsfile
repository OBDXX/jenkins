pipeline{
    agent any
    environment{
        DOCKERHUB_USERNAME = "oranbazak"
        REPO_NAME = "project"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${REPO_NAME}"
    }
    stages{
        stage('Docker login, build, tag and push'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker_hub_login_new', variable: 'docker_hub')]) {
                    sh """
                        docker build -t ${REPO_NAME}:$BUILD_ID .
                        docker image tag ${REPO_NAME}:$BUILD_ID ${IMAGE_NAME}:$BUILD_ID
                        docker login -u oranbazak -p ${docker_hub}
                        docker push ${IMAGE_NAME}:$BUILD_ID
                        """
                    }
                }
            }
        }
    }
}
