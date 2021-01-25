def dockerhub = "zayyanabdillah/jenkins"
def image_name = "${dockerhub}:${BRANCH_NAME}"
def builder

pipeline {
    agent any 

    // parameters {
    //     string(name: 'DOCKER_REPO', defaultValue: 'zayyanabdillah', description: 'docker repo address')
    //     booleanParam(name: 'PULL IMAGES', defaultValue: 'false', description: 'lorem ipsum')
    //     choice(name: 'DEPLOY', choices: ["PRODUCTION", "DEPLOYMENT"], description: 'lorem ipsum sit amet')
    // }

    stages {
        stage ("installing dependencies") {
            steps {
                nodejs("node14") {
                    sh 'yarn install'
                }
            }
        }
        stage ("build docker") {
            steps {
                script {
                    builder = docker.build("${dockerhub}:${BRANCH_NAME}")
                }
            }
        }
        stage ("test") {
            steps {
                script {
                    builder.inside {
                        sh "echo tested"
                    }
                }
            }
        }
        stage ("push image") {
            steps {
                script {
                    builder.push()
                }
            }
        }
        // stage ("deploy") {
        //     steps {
        //         script {
        //             sshPublisher {
        //                 publisher: [
        //                     sshPublisherDesc{
        //                         configName: "devops",
        //                         verbose: false,
        //                         transfer: [
        //                             sshTransfer(
        //                                 execCommand: "docker pull ${image_name; }"
        //                             )
        //                         ]
        //                     }
        //                 ]
        //             }
        //         }
        //     }
        // }
    }
}
