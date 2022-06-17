node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
  
       app = docker.build("amadouth/graphqll")
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    // stage('Trigger ManifestUpdate') {
    //             echo "triggering updatemanifestjob"
    //             build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
    //     }
    
    stage('Trigger Mise à jour du cluster Minikube') {
                echo "triggering updatemanifestjob"
                build job: 'Minikube cluster update', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
