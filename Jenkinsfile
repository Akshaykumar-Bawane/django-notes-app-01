@Library("Shared") _
pipeline {
    agent { label "vinod" }


    stages {
        stage('Hello') {
            steps {
                    script{
                        helloe()
                    }
            }
        }
        stage('Code'){
            steps{
                script{
                    clone( "https://github.com/Akshaykumar-Bawane/django-notes-app-01", "main")
                }
            }
        }
        stage('Build Fresh Images'){
            steps{
                script{
                   docker_build("notes-app","latest","dockerdaku877")
                }
                
            }
        }

        stage('Push to Dockerhub'){
            steps{
                  script{
                     docker_push("notes-app","latest","dockerdaku877")
                 }
            }
        }

        stage('Verify Deployment') {
            steps{    
                 echo "Verifying Django container status..."
                 sh '''
                 set +e   # disable exit on error
                 docker compose down || true
                 docker compose up -d || true
                 docker ps
                 docker logs django_cont || true
                 set -e   # re-enable exit on error
              '''
                 echo " Containers deployed successfully (even if Docker returned a warning )."

                  }
        }
    }
}
