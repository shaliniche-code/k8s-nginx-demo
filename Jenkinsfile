pipeline {
    agent any
    
    environment {
        IMAGE_NAME = "shalinidocker12/k8s-nginx-project"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        stage("git chkout") {
            steps {
                git branch: 'main',
                    credentialsId: 'github-creds',
                    url: 'https://github.com/shaliniche-code/k8s-nginx-demo.git'
            }
        }
        
         stage("Build docker image") {
             steps {
                 sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
             }
         }
         
         stage("Push docker image") {
             steps {
                 withCredentials([
                     usernamePassword(
                         credentialsId: 'dockerhubcreds', 
                         passwordVariable: 'DOCKER_PASSWORD', 
                         usernameVariable: 'DOCKER_USERNAME')]) {
                   sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'             
                   sh 'docker push ${IMAGE_NAME}:${IMAGE_TAG}'
}
             }
         }
         
         stage("Deploy to EKS") {
    steps {
        sh '''
            sed -i "s|IMAGE_PLACEHOLDER|${IMAGE_NAME}:${IMAGE_TAG}|" deployment.yml
            kubectl apply -f deployment.yml
            kubectl apply -f service.yml
            kubectl rollout status deployment/nginx-deployment
        '''
    }
}

    }
}
