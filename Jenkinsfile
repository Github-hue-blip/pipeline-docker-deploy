node{
    stage('scm checkout'){
        git branch: 'main', credentialsId: '1865689a-8b78-4368-a031-f45a808ae770', url: 'https://github.com/Github-hue-blip/pipeline-docker-deploy.git'
    }
    
    stage('maven build'){
        def mvnHome = tool name: 'Mvaen1', type: 'maven'
        
        def mvnCmd = "${mvnHome}/bin/mvn"
        
        sh "${mvnCmd} clean package" 
    }
    
    stage('build docker image'){
        withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
            sh 'docker login -u pavandocker2022 -p ${dockerhubpwd}'
        }
        
        sh 'docker build -t pavandocker2022/my-app:2.0.0 .'
    }
    
    stage('build docker image'){
        sh 'docker push pavandocker2022/my-app:2.0.0'
    }
    
    stage('run image on container'){
        
        def dockerRun = 'docker run -p 8089:8080 -d --name my-appc pavandocker2022/my-app:2.0.0'
        
        sshagent(['devserver-key']) {
            sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.21.125 ${dockerRun}"
        }
        
        
    }
    
    
}
