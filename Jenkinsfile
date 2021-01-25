def dockerhub = "zayyanabdillah/jenkins"
def images_name = "${dockerhub}:${BRANCH_NAME}"
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
        stage ("build") {
            steps {
                script {
                    builder = docker.build( images_name)
                }
            }
        }
        stage ("test") {
            steps {
                script {
                    builder.inside {
                        echo "inside image"
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
    }
}
