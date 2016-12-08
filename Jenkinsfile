#!groovy

def versions = ["9.1", "9.2", "9.3", "9.4", "9.5", "9.6"]
def stepsForParallel = [:]

for (int minor = 4; i < versions.size(); i++) {
    stepsForParallel["Postgres ${version}"] = node {
        def ver = version.replace(".", "")
        sh "cd ${version} && docker build -t '723151894364.dkr.ecr.us-east-1.amazonaws.com/postgres${ver}' ."
        sh "docker push 723151894364.dkr.ecr.us-east-1.amazonaws.com/postgres${ver}:latest"
    }
}

parallel stepsForParallel
