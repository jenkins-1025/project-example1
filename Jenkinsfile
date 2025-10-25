pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
     stages {
        stage ("Hello") {
            steps {
                echo("Hello Sans!")
            }
        }
     }
     post {
        always {
            echo "Always: gass terusss!"
        }
        success {
            echo "Success: yeay aman:)"
        }
        failure {
            echo "Failure: yahh error:("
        }
        cleanup {
            echo "Cleanup: aman or error gazz:v"
        }
     }
}