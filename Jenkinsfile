pipeline {
    agent {
        label {
        label "built-in"
        customWorkspace "/root/pramod/app"
        }
    }
    stages {
       stage ("clone") {
           steps {
               sh "cd /root/pramod/app"
               sh "rm -rf * "
                sh "git clone https://github.com/sunilpatil77/game-of-life.git"
            }
        }
        stage ("maven") {
            steps {
			dir ("/root/pramod/app/game-of-life") {
              	sh "mvn clean package"		
			
			dir ("gameoflife-web/target") {
                        sh "aws s3 cp gameoflife.war s3://sonu-bucket-77"
               	}
           	 	}
     	}
        }		
        stage ("deploy") {
            agent {
                node {
                    label "slave-one"
                }
            }
            steps {
                sh "aws s3 cp s3://sonu-bucket-77/gameoflife.war /server/tomcat/apache-tomcat-9.0.71/webapps"        
        	}
        }
    }
}
