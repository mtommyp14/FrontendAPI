def dockerhub = "mtommyp14/front"
def images_name = "${dockerhub}:${BRANCH_NAME}"
def builder 

pipeline{
    
    agent any

   parameters {
        string(name: 'DOCKERHUB', defaultValue: 'nameDockerID', description: 'DockerID')
        booleanParam(name: 'RUNTEST', defaultValue: 'false', description: 'Check to Runnig Test image')
        choice(name: 'DEPLOY', choices: ["main", "production"], description: 'Choice build to')
    }

    stages{

        stage("Install dependencies"){

            steps{
                nodejs("node14 front"){
                    sh 'yarn install'
                }
            }
        }
        
        stage("Main") {
           when {
                expression {
                    params.DEPLOY == "main"
                }
            }
            steps {
                    script {
                        builder = docker.build("${image_name}")
                    }
            }
        }


        stage("Production") {
           when {
                expression {
                    params.DEPLOY == "production"
                }
            }
            steps {
                    script {
                        builder = docker.build("${dockerhub}:${env.branch}")
                    }
            }
        }

        stage("Testing") {
            when {
                expression {
                    params.RUNTEST
                }
            }
            steps {
                 script {
                     builder.inside {
                         sh 'Success production'
                     }
                 }
            }
        }


        stage("Testing Image"){
            steps{
                script{
                    builder.inside{
                        sh 'passed'
                    }
                }
            }
        }

        stage("Push Image"){
            steps{
                script{
                        builder.push()
                    }
            }
        }

        

        stage("Deploy Main"){
            when {
                expression {
                    params.DEPLOY == "main"
                }
            }
            steps{
                script{
                    sshPublisher(
                        publishers: [
                            sshPublisherDesc(
                                configName: 'jenkinsever',
                                verbose: false,
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: 'docker-compose.yml',
                                        remoteDirectory: 'app',
                                        execCommand: "docker pull ${images_name}; docker kill frontendVue; docker run -d --rm --name frontendVue -p 8080:8080 ${images_name}",
                                        execTimeout: 1200000
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
        stage("Deploy Production"){
            when {
                expression {
                    params.DEPLOY == "production"
                }
            }
            steps{
                script{
                    sshPublisher(
                        publishers: [
                            sshPublisherDesc(
                                configName: 'jenkinsever',
                                verbose: false,
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: 'docker-compose.yml',
                                        remoteDirectory: 'app',
                                        execCommand: "docker pull ${images_name}; docker kill frontendVue; docker run -d --rm --name frontendVue -p 8080:8080 ${images_name}",
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