pipeline {
    agent any
    
    environment {
        GIT_REPO_LINK = 'https://github.com/rajibul2009/full-stack-mern-app.git'
        REPO_BRANCH = 'master'
    }

    stages {

        
        stage("Repo Clone") {
            steps {
                echo "Project Cloning..."
                git branch: "${env.REPO_BRANCH}", 
                    url: "${env.GIT_REPO_LINK}"
                sh "ls -lah"
            }
        }
    }
    
    post {
        always {
            echo 'This will always run after all the stages'
            echo 'Cleaning up workspace...'
            cleanWs()
        }
        failure {
            echo 'The build was successful.'
        }
        success {
            echo 'The build was successful.'
        }
    }
}