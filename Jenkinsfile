#!groovy

node {
    stage('Checkout') {
        checkout scm
    }

    def versions = ["9.4", "9.5", "9.6", "10"]
    def stepsForParallel = [:]

    for (int i =0; i < versions.size(); i++) {
        def version = versions[i]
        stepsForParallel["Postgres ${version}"] = {
            stage("Postgres ${version}"){
                def ver = "${version}".replace(".", "")
                sh "cd ${version} && docker build -t '723151894364.dkr.ecr.us-east-1.amazonaws.com/postgres${ver}' ."
                sh "docker push 723151894364.dkr.ecr.us-east-1.amazonaws.com/postgres${ver}:latest"
            }
        }
    }

    parallel stepsForParallel
}
