pipeline {
    agent any
    
    environment { 
      NAME = "myapp"
      VERSION = "${env.BUILD_ID}-${env.GIT_COMMIT}"
      //IMAGE = "${NAME}:${currentBuild.number}"   [we can use imagename:jenkins build number]
      //IMAGE = "${NAME}:${VERSION}"               [we can use imagename:git version number]
      IMAGE = "${NAME}:${currentBuild.number}"
   }

    stages {
        stage('workspace_cleanup') {
            steps {
                cleanWs()
            }
        }
        stage('clone') {
            steps {
                git branch: 'main', url: 'https://Naveen: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@github.com/snaveenkpn/Test2.git'
            }
        }
        stage('Docker_image') {
            steps {
               bat "docker build -t $IMAGE ."
            }
        }
        stage('providing Docker hub tag to image') {
            steps {
                bat "docker tag $IMAGE snaveenkpn/test:$currentBuild.number"
            }
        }
        stage('push image to docker hub') {
            steps {
                bat "docker push snaveenkpn/test:${currentBuild.number}"
            }
        }
    }
}
