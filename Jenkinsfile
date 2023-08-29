pipeline{
    agent any
    environment{
        DOCKERHUB_USERNAME = "oranbazak"
        //DOCKERHUB_LOGIN = "docker_hub_login"
        APP_NAME = "project"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
    }
    stages{
        stage('Docker login, build, tag and push'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker_hub_login_new', variable: 'docker_hub')]) {
                    sh """
                        docker build -t ${APP_NAME}:$BUILD_ID .
                        docker image tag ${APP_NAME}:$BUILD_ID ${IMAGE_NAME}:$BUILD_ID
                        docker image tag ${APP_NAME}:$BUILD_ID ${IMAGE_NAME}:latest
                        docker login -u oranbazak -p ${docker_hub}
                        docker push ${IMAGE_NAME}:$BUILD_ID
                        docker push ${IMAGE_NAME}:latest
                        """
                    }
                }
            }
        }
    }
}
