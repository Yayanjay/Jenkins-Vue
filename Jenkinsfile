def dockerhub = "zayyanabdillah/jenkins"
def image_name = "${dockerhub}:${BRANCH_NAME}"
def builder

pipeline {
    agent any 

    parameters {
        string(name: 'DOCKER_REPO', defaultValue: 'zayyanabdillah', description: 'docker repo address')
        booleanParam(name: 'PULL IMAGES', defaultValue: 'false', description: 'lorem ipsum')
        choice(name: 'DEPLOY', choices: ["PRODUCTION", "DEPLOYMENT"], description: 'lorem ipsum sit amet')
    }

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
        stage ("deploy") {
            steps {
                when {
                    expression {
                        params.DEPLOY == "DEPLOYMENT"
                    }
                }
                script {
                    sshPublisher (
                        publishers: [
                            sshPublisherDesc(
                                configName: 'devops',
                                verbose: false,
                                transfers: [
                                    sshTransfer(
                                        execCommand: "docker pull ${image_name}; docker kill vueapp; docker run -d --rm --name vueapp -p 8080:80 ${image_name}"
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
        stage ("production") {
            steps {
                when {
                    expression {
                        params.DEPLOY == "PRODUCTION"
                    }
                }
                script {
                    sshPublisher (
                        publishers: [
                            sshPublisherDesc(
                                configName: 'developer',
                                verbose: false,
                                transfers: [
                                    sshTransfer(
                                        execCommand: "docker pull ${image_name}; docker kill vueapp; docker run -d --rm --name vueapp -p 8080:80 ${image_name}"
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
    }
}
