pipeline {
    agent any
    
    environment {
        GIT_REPO_LINK = 'https://github.com/rajibul2009/full-stack-mern-app.git'
        REPO_BRANCH = 'master'
        
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh """
                    ls -lah
                    echo 'Hello Class'
                """
            }
        }
        stage("Repo Clone") {
            steps{
                echo "Project Cloning..."
                git url: "${GIT_REPO_LINK}"
                    branch: "${REPO_BRANCH}"
            
            sh "ls -lah"
            }
            
        }

        post {
        always {
            echo 'This will always run after all the stages'
            echo 'Cleaning up workspace...'
            cleanWs()
        }
        failure {
            echo 'The build has failed.'
        }
        success {
            echo 'The build was successful.'
        }
    }
}

}