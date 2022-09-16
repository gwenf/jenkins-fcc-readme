# Jenkins

Follow-along instructions for the freeCodeCamp Jenkins course.

Table of Contents

- [Technologies Used in Tutorial](#technologies)
- [Follow Along Material and Extra Information for Sections of the Course](#sections)
- [Extra Material](#extra-material)
- [Helpful Jenkins Resources](#helpful-jenkins-resources)
- [Related Projects](#related-projects)

## Overview

This is a tutorial showing how to build a CI/CD pipeline for a web application using Jenkins. I use one of my previous tutorial apps - [the Curriculum App](https://github.com/faraday-academy/curriculum-app) - from my livestreams to create this. One interesting thing about that app is that I already [have Github actions written to deploy it automatically to Dockerhub](https://github.com/faraday-academy/curriculum-app/tree/dev/.github/workflows) in the repo. That will give you an opportunity to compare the Jenkins pipeline I set up in this tutorial to an already working CI/CD pipeline in the repo.

## Technologies

- Debian servers running on Linode (Jenkins from Linode marketplace)
- Jenkins
- Docker & Dockerhub
- Github
- Some command line for settings things up

## Sections

*Every section here corresponds to a section in the freeCodeCamp video.*

### What is Jenkins?

Why would want you use Jenkins as an app developer?

- [Jenkins use cases](https://www.jenkins.io/solutions/)

Why do companies use Jenkins?

- [Jenkins users' YouTube playlist](https://www.youtube.com/playlist?list=PLN7ajX_VdyaNG5D3ERmAofba4-Fmqpe2i)

How does Jenkins compare to other CI/CD tools?

- [CI/CD Tools Comparison: Jenkins, GitLab CI, Buildbot, Drone, and Concourse](https://www.digitalocean.com/community/tutorials/ci-cd-tools-comparison-jenkins-gitlab-ci-buildbot-drone-and-concourse)
- [Comparing GitHub Actions vs Jenkins](https://acloudguru.com/blog/engineering/comparing-github-actions-vs-jenkins-ci-showdown)
- [Jenkins versus Gitlab](https://about.gitlab.com/devops-tools/jenkins-vs-gitlab/)
- [Aleternatives to Jenkins](https://alternativeto.net/software/jenkins/)

### Terms & Definitions

- [Jenkins official glossary of terms](https://www.jenkins.io/doc/book/glossary/)

### Project Architecture

![jenkins_architecture_balsamiq_diagram2](https://user-images.githubusercontent.com/10039233/190653544-48ea7cb1-bde8-4bf6-97b8-c1ff5bf854d2.png)

### Setting Up Linode

- [Signing up for Linode ($100 credit)](https://www.linode.com/students)
- [Jenkins in the Linode marketplace](https://www.linode.com/marketplace/apps/linode/jenkins/)

- Configuring Jenkins - admin account, plugins, settings
- Deploying an app to Github and using the Jenkins Github plugin  
- Using Jenkins to test and deploy to Dockerhub
- Another Linode server will be watching for updates on Dockerhub and pull & run the updated container  
- Reviewing Jenkins features like build history

### Setting Up Jenkins

**Make sure you follow these steps to set up Jenkins from the Linode marketplace**: https://www.linode.com/marketplace/apps/linode/jenkins/

- [Jenkins Handbook and Guides](https://www.jenkins.io/doc/book/)]

### Jenkins Plugins

- [Jenkins Plugin Index](https://plugins.jenkins.io/) - Search for plugins

### Blue Ocean UI

- [Blue Ocean Docs & Getting Started Guide](https://www.jenkins.io/doc/book/blueocean/)

### Jenkins Pipelines

Shell scripts from the tutorial:

```shell
ls -la

cd curriculum-front && npm i && npm run test:unit

docker build -f curriculum-front/Dockerfile . -t fuze365/curriculum-front

docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD

docker push fuze365/curriculum-front:latest
```

- [Getting started with Pipelines](https://www.jenkins.io/doc/book/pipeline/getting-started/)
- [In-Depth Pipeline Syntax](https://www.jenkins.io/doc/book/pipeline/syntax/)
- [Freestyle versus Pipeline Projects (old UI)](https://www.youtube.com/watch?v=IOUm1lw7F58)

### SSH'ing into Linode Servers (installing Git)

Commands for installing Git and Node on server:

```shell
# install Git
apt install git
git --version

# node version 16 (comes with npm)
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -
apt-get install -y nodejs
node --version
npm --version
```

- [Using the Lish Console](https://www.linode.com/docs/guides/using-the-lish-console/)
- [Official video on how to SSH into Linode server](https://www.youtube.com/watch?v=ZVMckBHd7WA)
- [SSH into Linode server articles](https://www.linode.com/docs/guides/networking/ssh/)

- [How to install Git on Linux](https://www.linode.com/docs/guides/how-to-install-git-on-linux-mac-and-windows/)
- [How to install Node with npm on Linux](https://www.linode.com/docs/guides/install-and-use-npm-on-linux/)

### Jenkinsfile

- [Using a Jenkinsfile](https://www.jenkins.io/doc/book/pipeline/jenkinsfile/)
- [Deep Dive into a Jenkinsfile video](https://www.youtube.com/watch?v=7KCS70sCoK0&list=PLy7NrYWoggjw_LIiDK1LXdNN82uYuuuiC&index=6)

### Docker & Dockerhub

- [Sign up for an account on Dockerhub](https://hub.docker.com/)

## Extra Material

There are two main ways to handle app deployments with our Jenkins setup:

1. We could deploy the app to Dockerhub and have the app server watch for changes to the docker image. It will pull whenever there are changes. (this is what we have set up now)
2. The more advanced setup is to have Jenkins deploy directly to our app server when all of the CI steps pass. This requires a bit of extra configuration in Jenkins and also ensuring security in the app server.

You can [see this tutorial](https://www.youtube.com/watch?v=hf8wUUrGCgU) for a walkthrough of how I set up the app server to watch for changes to a Docker image on Dockerhub.

## Helpful Jenkins Resources

- [Linode YouTube channel](https://www.youtube.com/c/linode)
- [Official Jenkins YouTube channel](https://www.youtube.com/c/jenkinscicd/playlists)
- [TechWorld with Nana YouTube channel](https://www.youtube.com/c/TechWorldwithNana/search?query=jenkins)
- [Cloudbees YouTube channel](https://www.youtube.com/c/CloudBeesTV/search?query=jenkins)

## Related Projects

- [Jenkins X](https://jenkins-x.io/)
