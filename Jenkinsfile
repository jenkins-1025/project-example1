pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
     stages {
        stage ("Build") {
            steps {
                echo("Hello Build 1!")
                echo("Hello Build 2!")
            }
        }
        stage ("Test") {
            steps {
                echo("Hello Test A")
                //sh("error")
            }
        }
        stage ("Deploy") {
            steps {
                echo("Hello Deploy I")
                echo("Hello Deploy II")
                echo("Hello Deploy III")
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