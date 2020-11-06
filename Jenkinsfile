#!groovy

node {
    stage('Checkout') {
        checkout scm
    }

    def versions = ["9.5", "9.6", "10", "11", "12", "13"]
    def stepsForParallel = [:]

    for (int i =0; i < versions.size(); i++) {
        def version = versions[i]
        stepsForParallel["Postgres ${version}"] = {
            stage("Postgres ${version}"){
                def ver = "${version}".replace(".", "")
                // Pull the latest image so we have a record of the sha
                sh "docker pull 723151894364.dkr.ecr.us-east-1.amazonaws.com/postgres${ver}:latest || true"

                sh "docker build -t '723151894364.dkr.ecr.us-east-1.amazonaws.com/postgres${ver}' ${version}/"
                if (env.BRANCH_NAME == 'master') {
                    //# Try to create the repository so the push doesn't fail
                    sh "aws ecr create-repository --repository-name postgres${ver} || true"

                    sh "docker push 723151894364.dkr.ecr.us-east-1.amazonaws.com/postgres${ver}:latest"
                }
            }
        }
    }

    parallel stepsForParallel
}
