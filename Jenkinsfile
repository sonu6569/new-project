pipeline {
    agent any

    // Define the environment variables
    environment {
        GIT_BRANCH = 'main' // Change this to the desired branch name
    }
    // running container stop
    stages {
    stage ('docker-container-stop') {
    steps {
          sh 'docker stop workpress_app'
          sh 'docker remove wordpress_app'
}
}
        stage('Checkout') {
            steps {
                // Clean workspace and checkout the repository
                cleanWs()
                checkout scm
            }
        }

        stage('Git Pull') {
            when {
                // Trigger the stage only when changes are pushed to the main branch
                branch 'main'
                changeset '.*'
            }
            steps {
                script {
                    // Get the latest changes from the remote main branch
                    sh "git pull origin ${env.GIT_BRANCH}"
                }
            }
       // start container
        stage('start-container') {
        steps {

             sh 'docker run -it --network my_network  wordpress_app'
}
    
}

        }	

    
    }
}      
        	}
        }
    }
}
