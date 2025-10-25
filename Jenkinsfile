pipeline {
    agent none
    /*
    agent {
        node {
            label "linux && java11"
        }
    }
    */
     stages {
        stage ("Build") {
            agent {
                node {
                label "linux && java11"
                }
            }
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
                script {
                    for (int i = 0; i < 10; i++) {
                        echo("Script ${i}")
                    }
                }
                //sh("error")
            }
        }
        stage ("Deploy") {
            steps {
                echo("Hello Deploy ")
                script{
                    def data = [
                        "firstName": "M.",
                        "lastName": "Hasan"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
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