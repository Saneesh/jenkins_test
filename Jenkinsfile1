pipeline {
   agent any
   
   stages {
       stage('Setup Parameter') {
           steps {
                  script {
                       properties([
                           parameters([
                                choice(
                                   choices: ["dev", "uat", "prod"],
                                   name: "ENVIRONMENT"
                                   )
                            ])
                       ])
                    }
               }
         } 
         stage('print parameter') {
              steps {
                 echo "$ENVIRONMENT"
                 }
          }
    }
}
