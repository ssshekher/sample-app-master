pipeline {


    agent none
    stages {
       
        stage('Build') {
            
            agent {
               docker {
      
                  image 'python:2-alpine'
                }
              }
             
             steps {
    
                sh 'python -m py_compile src/main.py'
   
                stash(name: 'compiled-results' , includes: 'src/*.py*')
             }
         }
         stage('Deliver') {
                  agent any
                  environment {
                      VOLUME = '$(pwd)/src:/src'
                      IMAGE = 'cdrx/pyinstaller-linux:python2'
                   }
                   steps {
                       dir(path: env.BUILD_ID) {
                           unstash(name: 'compiled-results')
                            sh "docker run --rm -v ${VOLUME} ${IMAGE} 'pyinstaller -F main.py'"
                        }
                     }
                     post {
                        success {
                            archiveArtifacts "${env.BUILD_ID}/sources/dist/main"
                            sh "docker run --rm -v ${VOLUME} ${IMAGE} 'rm -rf build dist' "
                         }
                     }
 
        
                 }

       }
    } 
    
