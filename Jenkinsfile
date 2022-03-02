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
        
          stage('Test') {
                     agent {
                         docker {

                           image 'qnib/pytest'
                          }
                      }
                       steps {


                         .sh 'py.test --verbose --junit-xml test-reports/results.xml src/main.py'

                       }
                      post {
                         always {
                            
                            junit 'test-reports/results.xml'
                      }
                  }
            }


       }
    } 
    
