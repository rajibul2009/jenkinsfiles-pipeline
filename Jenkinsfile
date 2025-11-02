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
                git url: "${GIT_REPO_LINK}", branch: "${REPO_BRANCH}"
                sh "ls -lah"
                echo "Check inside run_mern_stack_with_docker_compose directory"

                dir("run_mern_stack_with_docker_compose") {
                    sh "ls -lah"
                    dir("frontend"){
                        sh "ls -lah"
                    }
                }

            }
        }

        stage("Prepare docker-compose file") {
            steps {
                echo " Preparing docker-compose.yaml..."
                dir("run_mern_stack_with_docker_compose") {
                    sh """
                    ls -lah
                    rm docker-compose.yaml
                    ls -lah
                   """
                    writeFile file: 'docker-compose.yaml', text: """
services:
  # React Frontend Service
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
    container_name: frontend-app
    restart: unless-stopped
    ports:
      - "5000:5000"
    environment:
      - VITE_API_URL=http://192.168.224.130:3000/api 
    networks:
      - todo_network 

networks:
  todo_network:
    name: todo_network
    external: true
"""
                }
            }
        }

        stage("Docker image build") {
            steps {
                echo "Docker image - build the services"
                dir("run_mern_stack_with_docker_compose") {
                    sh """
                        ls -lah
                        docker compose build
                    """
                }
            }
        }
        stage("Docker Compose down"){
            steps {
                echo "Docker Compose - down the existing services"
                dir("run_mern_stack_with_docker_compose") {
                    sh """
                        ls -lah
                        docker compose down
                    """
                }
            }
        }
        stage("Docker Compose up - detached mode"){
            steps {
                echo "Docker Compose - up the services in detached mode"
                dir("run_mern_stack_with_docker_compose") {
                    sh """
                        ls -lah
                        docker compose up -d
                    """
                }
            }
        }
    }

    post {
        always {
            echo ' Cleaning workspace...'
            cleanWs()
        }
        failure {
            echo ' Build failed.'
        }
        success {
            echo 'Build successful!'
        }
    }
}
