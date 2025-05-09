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
                             sh 'sudo docker tag tomcat:$BUILD_TAG karanjangid12/docker-pipeline:$BUILD_TAG'
                             }
                }
                
        }
}

