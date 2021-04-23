pipeline {

  agent any

  stages {
    stage('Build') {
        agent any
        steps {
            echo 'compiling...'
        }
    }
    stage ('Deploy To Prod'){
        input{
          message "Do you want to proceed for production deployment $aplicacion ?"
        }
        steps {
            sh 'echo "Deploy into Prod"'
        }
      }

    stage('Deploy') {

      when {

        expression {

          openshift.withCluster() {

            return !openshift.selector('bc', 'quarkus2').exists();

          }

        }

      }

      steps {

        script {

          openshift.withCluster() {

            openshift.newApp('openjdk-11:1.3 https://github.com/trixlan/blue.git', '--name=quarkus').narrow('svc').expose()
          }

        }

      }

    }

  }

}
