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
       }
    } 
    
