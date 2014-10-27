---
layout: post
author: absolut
title: Running Jenkins via boot2docker
---

If you have public projects and you want to do CI for this projects, you can use tools like [TravisCI](https://travis-ci.org/).

For small private projects you can setup a private jenkins instance. A simple way to do this is by using docker.


Installing
--------

* Install / Update [boot2docker](http://boot2docker.io/)
* Make sure you can access boot2docker by executing `docker images` (If you are sure boot2docker is running but you get an error message, try executing `$(boot2docker shellinit)`)
* Download the latest jenkins docker image: `docker pull jenkins`
* Test if jenkins can be started by 
	* executing `docker run -p 8080:8080 jenkins`
	* When the VM is running, execute `boot2docker ip` and try opening the URL `http://<IP returned by boot2docker ip>:8080`
	* Now you should see the Jenkins interface



Since we did not mount any host folder to the jenkins instance, we need to setup this binding so all job configurations / plugins / etc. are persistent. With boo2docker, mounting host folders to docker images has become very [easy](https://blog.docker.com/2014/10/docker-1-3-signed-images-process-injection-security-options-mac-shared-directories/): 
 
* Create a folder on your mac (e.g. `/opt/development/jenkins_home`)
* Stop the jenkins image
* Start the image by executing `docker run -p 8080:8080 -v /opt/development/jenkins_home:/var/jenkins_home jenkins`
* Access the jenkins instance by opening the URL  `http://<IP returned by boot2docker ip>:8080`
* Make sure the folder mounting works as expected: The folder on your Mac should now contain some files created by jenkins.

Upgrading
-------

* Stop your jenkins instance
* execute `docker pull jenkins`
* Now you can start up jenkins again as described above





