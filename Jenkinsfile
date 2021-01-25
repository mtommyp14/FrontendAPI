def dockerhub = "mtommyp14/front"
def images_name = "${dockerhub}:${BRANCH_NAME}"
def builder 

pipeline{
    
    agent any

    stages{

        stage("Install dependencies"){

            steps{
                nodejs("node14 front"){
                    sh 'yarn install'
                }
            }
        }

        stage("Build Docker"){
            steps{
                script{
                    builder = docker.build("${dockerhub}:${BRANCH_NAME}")
                }
            }
        }

        stage("Testing Image"){
            steps{
                script{
                    builder.inside{
                        sh 'echo passed'
                    }
                }
            }
        }

        // stage("Push Image"){
        //     steps{
        //         script{
        //                 builder.push()
        //             }
        //     }
        // }



        stage("Deploy"){
            steps{
                script{
                    sshPublisher(
                        publishers: [
                            sshPublisherDesc(
                                configName: 'jenkinserver',
                                verbose: false,
                                transfers: [
                                    sshTransfer(
                                        execCommand: "docker-compose up -d",
                                        execTimeout: 1200000
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