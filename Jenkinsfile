pipeline {
    agent none
    /*agent {
        node {
            label "linux && java11"
        }
    }*/
    environment {
        AUTHOR = "M. Hasan"
        EMAIL = "hasanmuhammad197@gmail.com"
    }
    options {
        disableConcurrentBuilds()
        timeout(time:10, unit:'MINUTES')
    }
     stages {
        stage ("Prepare") {
            environment {
                AUTH = credentials("mhasan_secret")
            }
            agent {
                node {
                label "linux && java11"
                }
            }
            steps {
                echo("Author : ${AUTHOR}")
                echo("Email : ${EMAIL}")
                echo("Auth user : ${AUTH_USR}")
                echo("Auth password : ${AUTH_PSW}")
                //sh("echo 'Auth password : ${AUTH_PSW}' > 'secret.txt'") //detect warning Groovy String Interpolation
                sh('echo "Auth password : ${AUTH_PSW}" > "secret.txt"')
                echo("Start job : ${env.JOB_NAME}")
                echo("Start build : ${env.BUILD_NUMBER}")
                echo("Branch name : ${env.BRANCH_NAME}")
            }
        }
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
            agent {
                node {
                label "linux && java11"
                }
            }
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
            agent {
                node {
                label "linux && java11"
                }
            }
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