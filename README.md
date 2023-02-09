# dockerSandbox
Trying to build better images for my projects.

I know from experience that workflow assumptions and dockerfile practices can materially impact image size and operational performance.  

This repo is an attempt to persist a few of my attempts to optimize my Docker-related activities.  

For an abbreviated *course* on simplistic example for your development, see: "[How To Use Docker To Make Local Development A Breeze.](https://www.youtube.com/watch?v=zkMRWDQV4Tg)" and its supporting code at [https://github.com/ArjanCodes/2022-docker](https://github.com/ArjanCodes/2022-docker)  

### Reminders:  
* Use a linter on all Dockerfiles -- for example [hadolint](https://github.com/hadolint/hadolint) or [another alternative](https://github.com/hadolint/hadolint#alternatives) (*because 'hope' is not a practical risk management strategy*). See a brief hadolint overview/how-to at [https://www.howtogeek.com/devops/how-to-use-hadolint-to-lint-your-dockerfiles/](https://www.howtogeek.com/devops/how-to-use-hadolint-to-lint-your-dockerfiles/)  
* Using multi-stage builds (*lots of layers*) can result in large docker images.  
* For Python applications, you might consider using venv early in the build and then copy the virtual environment directory to another subsequent, much lighter image like python:3.10-slim-buster. Caution: <version>-slim* images do not contain all the common packages contained in the default tag and hosts only the minimal packages needed to run python.  
* I also need to research [docker-slim](https://hub.docker.com/r/dslim/docker-slim)/[SlimToolkit](https://slimtoolkit.org/) for managing the lifecycle of multi-stage images, as it appears to make spectacular size reductions for some images (*with some risk management advantages as well*)  
* I sometimes use _____:latest, and need to specify images more narrowly... Testing with python:3.6 and python:3.11 may produce different results.  
* Use docker-compose more routinely.  
* Investigate building with [Kaniko](https://cloud.google.com/blog/products/containers-kubernetes/introducing-kaniko-build-container-images-in-kubernetes-and-google-container-builder-even-without-root-access) instead of docker-compose or docker build.  Because it does not depend on Docker daemons, it may have a reduced attack surface, and may include other advantages as well (*speed, size, etc.*).  See: [https://www.baeldung.com/ops/kaniko](https://www.baeldung.com/ops/kaniko) and [https://github.com/GoogleContainerTools/kaniko](https://github.com/GoogleContainerTools/kaniko) as well.  



