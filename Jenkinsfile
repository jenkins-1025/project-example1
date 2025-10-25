pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
     stages {
        stage ("Build") {
            steps {
                echo("Hello Build!")
            }
        }
        stage ("Test") {
            steps {
                echo("Hello Test!")
            }
        }
        stage ("Deploy") {
            steps {
                echo("Hello Deploy!")
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