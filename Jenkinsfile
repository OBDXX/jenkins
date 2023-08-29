pipeline{
    agent any
    environment{
        //user and repo
        DOCKERHUB_USERNAME = "oranbazak"
        REPO_NAME = "project"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${REPO_NAME}"
    }
    stages{
        stage('Docker login, build, tag and push'){
            steps{
                script{ //The credentials I stored in the jenkins (password)
                    withCredentials([string(credentialsId: 'docker_hub_login_new', variable: 'docker_hub')]) {
                    //Scripts
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
        stage('Docker pull and run curl test'){
            steps{
                script{
                    sh '''
                            docker run -d --name $BUILD_ID ${IMAGE_NAME}:$BUILD_ID
                        '''
                }
            }
        }
    }
}
