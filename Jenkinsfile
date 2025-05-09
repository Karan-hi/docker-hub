pipeline {
        agent {
               label 'slave1'
               }
        stages {
                stage("SCM") {
                     steps {
                            git 'https://github.com/Karan-hi/docker-hub.git'
                            }
                          }

                stage("build") {
                     steps {
                             sh 'sudo mvn clean package'
                             }
                           }
                stage("build-image") {
                     steps {
                             sh 'sudo docker build -t tomcat:$BUILD_TAG .'
                             sh 'sudo docker tag tomcat:$BUILD_TAG technetgalaxy/pipeline-java:$BUILD_TAG'
                             }
                }
                stage("dockerlogin") {
                     steps { 
		             withCredentials([string(credentialsId: 'docker-hub-passwd', variable: 'dockerhub-passwd-var')]) {
			     sh 'sudo docker login -u karanjangid12 -p ${dockerhub-passwd-var}'
			     sh 'sudo docker push karanjangid12/pipeline-java:$BUILD_TAG'
			     }
		     }
		      
		} 
		stage("QAT TESTING") {
		     steps {  
		              sh 'sudo docker rm -f $(sudo docker ps -a -q)'
 
		              sh 'sudo docker run -dt --name web3tom -p 8085:8080 technetgalaxy/pipeline-java:$BUILD_TAG'
                    }
	    }
        }
}

