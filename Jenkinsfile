pipeline{
    agent any
    stages{
        stage('fetch git repo code'){
            steps{
                echo 'create stage 1 fetch git repo code'
                git branch 'springboot', url:'https://github.com/Revatipati/unidevsecops.git'
                sh 'ls'
            }

        }
    }
}