# <https://github.com/plangrid/postgres>

## PlanGrid Postgres Fork
This repo has been forked from [docker-library/postgres](https://github.com/docker-library/postgres) and customized for the ADSK / PlanGrid usage.

Notable changes include:

* Debian files
  * Installation of the [HyperLogLog (HLL) extension](https://github.com/citusdata/postgresql-hll) as required by plangrid-insights.
  * Removal of volume for data as this does not get cleaned up when the container is torn down (see PlanGrid: DEVOPS-620).
* Note: Alpine files have not been updated.
* Removal of `./github/workflows/` files to prevent unnecessary GitHub CI builds for this fork.
* Jenkins build file for pushing images to ECR.

### Upstream updates

```zsh
# Create an update branch
$ git checkout master
$ git pull
$ git checkout -b my_update_branch

# Merge the update branch with the upstream repo
$ git remote add upstream git@github.com:docker-library/postgres.git
$ git fetch upstream
$ git merge upstream/master
```

### Manual testing

```zsh
# Build the image
$ docker build -t plangrid_postgres_12 12/

# Run the image
$ docker run -dp 15432:5432 -e POSTGRES_PASSWORD=password123 plangrid_postgres_12

# Connect to the database
$ psql "postgres://postgres:password123@localhost:15432"

-- Verify the version
postgres=# SELECT version();

-- Verify that the hll extension can be created
postgres=# CREATE EXTENSION hll;

-- Verify that the Encoding and Collate is en_US.utf8
postgres=# \l
```

---

## https://github.com/docker-library/postgres

## Maintained by: [the PostgreSQL Docker Community](https://github.com/docker-library/postgres)

This is the Git repo of the [Docker "Official Image"](https://github.com/docker-library/official-images#what-are-official-images) for [`postgres`](https://hub.docker.com/_/postgres/) (not to be confused with any official `postgres` image provided by `postgres` upstream). See [the Docker Hub page](https://hub.docker.com/_/postgres/) for the full readme on how to use this Docker image and for information regarding contributing and issues.

The [full image description on Docker Hub](https://hub.docker.com/_/postgres/) is generated/maintained over in [the docker-library/docs repository](https://github.com/docker-library/docs), specifically in [the `postgres` directory](https://github.com/docker-library/docs/tree/master/postgres).

## See a change merged here that doesn't show up on Docker Hub yet?

For more information about the full official images change lifecycle, see [the "An image's source changed in Git, now what?" FAQ entry](https://github.com/docker-library/faq#an-images-source-changed-in-git-now-what).

For outstanding `postgres` image PRs, check [PRs with the "library/postgres" label on the official-images repository](https://github.com/docker-library/official-images/labels/library%2Fpostgres). For the current "source of truth" for [`postgres`](https://hub.docker.com/_/postgres/), see [the `library/postgres` file in the official-images repository](https://github.com/docker-library/official-images/blob/master/library/postgres).

---

-	[![build status badge](https://img.shields.io/github/workflow/status/docker-library/postgres/GitHub%20CI/master?label=GitHub%20CI)](https://github.com/docker-library/postgres/actions?query=workflow%3A%22GitHub+CI%22+branch%3Amaster)
-	[![build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/update.sh/job/postgres.svg?label=Automated%20update.sh)](https://doi-janky.infosiftr.net/job/update.sh/job/postgres/)

| Build | Status | Badges | (per-arch) |
|:-:|:-:|:-:|:-:|
| [![amd64 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/amd64/job/postgres.svg?label=amd64)](https://doi-janky.infosiftr.net/job/multiarch/job/amd64/job/postgres/) | [![arm32v5 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm32v5/job/postgres.svg?label=arm32v5)](https://doi-janky.infosiftr.net/job/multiarch/job/arm32v5/job/postgres/) | [![arm32v6 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm32v6/job/postgres.svg?label=arm32v6)](https://doi-janky.infosiftr.net/job/multiarch/job/arm32v6/job/postgres/) | [![arm32v7 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm32v7/job/postgres.svg?label=arm32v7)](https://doi-janky.infosiftr.net/job/multiarch/job/arm32v7/job/postgres/) |
| [![arm64v8 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm64v8/job/postgres.svg?label=arm64v8)](https://doi-janky.infosiftr.net/job/multiarch/job/arm64v8/job/postgres/) | [![i386 build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/i386/job/postgres.svg?label=i386)](https://doi-janky.infosiftr.net/job/multiarch/job/i386/job/postgres/) | [![mips64le build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/mips64le/job/postgres.svg?label=mips64le)](https://doi-janky.infosiftr.net/job/multiarch/job/mips64le/job/postgres/) | [![ppc64le build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/ppc64le/job/postgres.svg?label=ppc64le)](https://doi-janky.infosiftr.net/job/multiarch/job/ppc64le/job/postgres/) |
| [![s390x build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/s390x/job/postgres.svg?label=s390x)](https://doi-janky.infosiftr.net/job/multiarch/job/s390x/job/postgres/) | [![put-shared build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/put-shared/job/light/job/postgres.svg?label=put-shared)](https://doi-janky.infosiftr.net/job/put-shared/job/light/job/postgres/) |

<!-- THIS FILE IS GENERATED BY https://github.com/docker-library/docs/blob/master/generate-repo-stub-readme.sh -->
