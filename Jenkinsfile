pipeline {
    agent any

    parameters {        
        string(name: 'dockerHubUserName', defaultValue: 'userName', description: 'UserName for docker hub')
        password(name: 'dockerHubPassword', defaultValue: 'SECRET', description: 'password for dockerhub')    
        string(name: 'dockerImageNameApp', defaultValue: 'imageName', description: 'image name for spp')
        string(name: 'dockerVersionApp', defaultValue: '1.0', description: 'docker image version for app')
    }

    environment {
        AppDockerFile = './application-tier'
        AppImageName=''
    }
    stages {
    stage('Login Docker') {
        steps {
            sh 'docker login -u ${dockerHubUserName} -p ${dockerHubPassword}'
        }
    }

    stage('Build Docker Image For App Tier') {
        steps {
             
            
            sh 'docker build -t ${dockerImageNameApp}:${dockerVersionApp} ${AppDockerFile}'
        }
    }
 
    stage('Push Docker App Image') {
        steps {
            sh 'docker tag ${dockerImageNameApp}:${dockerVersionApp} ${dockerHubUserName}/${dockerImageNameApp}:${dockerVersionApp} && docker push ${dockerHubUserName}/${dockerImageNameApp}:${dockerVersionApp}'
            script {
                    AppImageName='${dockerHubUserName}/${dockerImageNameApp}:${dockerVersionApp}'
                echo '${AppImageName}'
                }
        }
    }
     
    }
}
