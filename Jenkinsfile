node {
    def app
    stage('Clone repository') {
        checkout main
    }
    stage('Build image') {
       app = docker.build("lkolev/kiii-jenkins-blueocean")
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}
