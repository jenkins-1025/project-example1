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
    //triggers {
        //cron("*/5 * * * *")
        //pollSCM("* * * * *")
        //upstream(upstreamProjects: 'job1,job2', threshold: hudson.model.Result.SUCCESS)
    //}
    parameters {
        string(name:"NAME", defaultValue:"Guest", description:"What is your name?")
        text(name:"DESCRIPTION", defaultValue:"Guest", description:"Tell me about you?")
        booleanParam(name:"DEPLOY", defaultValue:false, description:"Need to deploy?")
        choice(name:"SOCIAL_MEDIA", choices:['Instagram','Facebook','Twitter'], description:"What is your social media?")
        password(name:"SECRET", defaultValue:"", description:"Encrypt Key")
    }
    options {
        disableConcurrentBuilds()
        timeout(time:10, unit:'MINUTES')
    }
     stages {
        stage ("OS Setup") {
            matrix {
                axes {
                    axis {
                        name "OS"
                        values "linux", "windows", "mac"
                    }
                    axis {
                        name "ARC"
                        values "32", "64"
                    }
                }
                stages {
                    stage("OS Setup") {
                        agent {
                            node {
                                label "linux && java11"
                            }
                        }
                        steps {
                            echo "Setup for ${OS} ${ARC}"
                        }
                    }
                }
                excludes {
                    exclude {
                        axis {
                            name "OS"
                            values "mac"
                        }
                        axis {
                            name "ARC"
                            values "32"
                        }
                    }
                }
            }
        }
        stage ("Conditional") {
            parallel {
                stage("Conditional 1") {
                    agent {
                         node {
                         label "linux && java11"
                         }
                    }
                    steps {
                        echo("Conditional 1")
                    }
                }
                stage("Conditional 2") {
                    agent {
                         node {
                         label "linux && java11"
                         }
                    }
                    steps {
                        echo("Conditional 2")
                    }
                }
            }
        }
        stage ("Parameter") {
            agent {
                node {
                label "linux && java11"
                }
            }
            steps {
                echo "Hello ${params.NAME}"
                echo "Your description is ${params.DESCRIPTION}"
                echo "Your social media is ${params.SOCIAL_MEDIA}"
                echo "Need to deploy : ${params.DEPLOY} to deploy!"
                echo "Your secret is ${params.NAME}"
            }
        }
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
                echo("Pause build 3s...")
                sleep(3)
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
                    for (int i = 0; i < 3; i++) {
                        echo("Script ${i}")
                    }
                }
                //sh("error")
            }
        }
        stage ("Deploy") {
            input {
                message "Mau deploy?"
                ok "Yeah, deploy sekarang"
                submitter "hasan, user"
                parameters {
                    choice(name: "ENV_TARGET", choices: ['DEVEL','STAGING','PRODUCTION'], description: "Pilih Environment?")
                }
            }
            agent {
                node {
                label "linux && java11"
                }
            }
            steps {
                echo("Hello Deploy ")
                echo("Already Deploy to ${ENV_TARGET} ")
                script{
                    def data = [
                        "firstName": "M.",
                        "lastName": "Hasan"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
            }
        }
        stage ("Release") {
            when {
                expression {
                    return params.DEPLOY
                }
            }
            agent {
                node {
                label "linux && java11"
                }
            }
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "mhasan_secret",
                    usernameVariable: "USER",
                    passwordVariable: "PASSWORD"
                )]) {
                    sh('echo "Release success with -u $USER -p $PASSWORD" > "release.txt"')
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