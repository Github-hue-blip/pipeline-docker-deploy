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
        sh 'docker build -t pavandocker2022/my-app:2.0.0 .'
    }
    
    
}
