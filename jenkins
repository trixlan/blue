pipeline {

  agent any

  stages {

    stage('Build') {

      when {

        expression {

          openshift.withCluster() {

            return !openshift.selector('bc', 'quarkus').exists();

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
