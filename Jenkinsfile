pipeline{
    agent any
    stages{
        stage('fetch git repo code'){
            steps{
                echo 'create stage 1 fetch git repo code'
                git branch: 'springboot', url:'https://github.com/Revatipati/unidevsecops.git'
                sh 'ls'
            }

        }
        stage('SAST using trivy for vuln scaning'){
            steps{
                echo 'SAST using trivy for vuln'
                sh 'trivy fs --scanners vuln,secret,misconfig .'            
            }
            
        }
        stage('compsoe for build and curl for app status test') {
            steps {
                echo 'running docker compose'
                sh 'docker-compose down'
                sh 'docker-compose up -d --build'
                sh 'docker-compose ps'
                //sh 'curl -f http://localhost:3001'
            }
            
        }
        // using docker pipeline to build and push 
        stage('building image and pushing it') {
            steps {
                echo 'using docker pipeline plugin to build and push image'
                script {
                    def imageName = "revatipatic1/srpingapp"
                    def imageTag  = "tomactdep$BUILD_NUMBER"
                    def ashuCred = "d1b1914d-6a37-4bd6-8212-b3e499dba22a"
                    // building image 
                    docker.build(imageName + ":" + imageTag , " -f Dockerfile .")
                    // pushing image 
                    docker.withRegistry('https://registry.hub.docker.com',ashuCred){
                        docker.image(imageName + ":" + imageTag).push()
                    }
                }
            }
        }
        stage('chck conn kubectl'){
            steps{
                echo 'kubectl version cmd'
                sh 'kubectl get nodes'
                sh 'kubectl version'
            }

        }
        stage('deployment'){
            steps{
                echo 'deployment'
                sh 'kubectl apply -f deploy1.yaml -f service.yaml'
                sh 'kubectl get deploy,pod,service'
            }
          
    
    stage('upgrade'){
        steps{
            echo 'upgrade'
            sh 'kubectl set image deployment chrp-tomcat chrpjava=revatipatic1/srpingapp:tomcatdeploy$BUILD_NUMBER'
        }

    }
    }

}