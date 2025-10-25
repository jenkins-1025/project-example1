pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
     stages {
        stage ("Build") {
            steps {
                echo("Start build...")
                echo("Pause build 10s...")
                sleep(10)
                sh("./mvnw clean compile test-compile")
                echo("Finish build...")
            }
        }
        stage ("Test") {
            steps {
                echo("Hello Test A")
                sh("./mvnw test")
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