pipeline{
    agent any
    stages{
        stage('fetch git repo code'){
            steps{
                echo 'fetch git repo code'
                git branch 'springboot', url:'https://github.com/Revatipati/unidevsecops.git'
                sh 'ls'
            }

        }
    }
}