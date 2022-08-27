pipeline {
   agent { 
         label { label 'built-in'
		 }
   }
  
  stages {
  
  stage ('clone-git-repo') {
  
  steps {
        dir ('/mnt/') {
		sh 'rm -rf game-of-life'
        sh'git clone  https://github.com/AwsDevop013/game-of-life.git '
		   }
         }
		} 
    stage ('maven-install') {
  
  steps {
  
        dir ('/mnt/game-of-life/') {
        sh'mvn install'
		}
        }
    }
 stage ('upload-s3') {
  
  steps {
        sh'aws s3 cp /mnt/game-of-life/gameoflife-web/target/gameoflife.war s3://melody-chocolaty '
		
    }
   }
    stage ('delpoy') {
	
	agent {
	        node {
                  label 'DEV-1'
			} 
  }
  steps {
         sh 'aws s3 cp s3://melody-chocolaty/gameoflife.war /mnt/webserver/apache-tomcat-9.0.65/webapps '
    }
   }
  }
 }

zbc
