pipeline {
    agent any
    tools {
        maven "Maven3"
    }
    stages {
        stage ('Checkout SCM'){
            steps {
              checkout([$class: 'GitSCM', branches: [[name: '*/master']],
    			userRemoteConfigs: [[url: 'https://github.com/chdattat/Java-sample-docker.git']]])
            }
        }
          
         stage ('Build')  {
            steps {
        	    sh "mvn package"
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "ls -a"
                sh "docker build -t webapptest:${env.BUILD_ID} ."
            }
        }
    }
}
