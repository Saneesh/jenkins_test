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
                                   ),
                                string(
                                    defaultValue: "training",
                                    name: "STRING")
                            ])
                       ])
                    }
               }
         } 
         stage('print parameter') {
              steps {
                 echo "Choice parameter is $ENVIRONMENT"
                 echo "String parameter is $STRING"
                 }
          }
    }
}
