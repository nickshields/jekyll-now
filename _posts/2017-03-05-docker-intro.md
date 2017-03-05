---
layout: post
title: Setting up Docker for Development
---
![_config.yml]({{ site.baseurl }}/images/docker.png)

Although Docker is extremely well documented, I still feel that it's necessary for me to blog my experiences.
Especially after going through the initial setup for getting ready to develop. For anyone who's looking to follow along,
please visit the Docker [Documentation.](https://docs.docker.com/opensource/project/who-written-for/)

The first steps to getting ready for docker development seem trivial. 
* Create a Github Account
* Install Git
* Install Make
* Install Docker

I should make everyone aware that I am developing on a Mac, to clear up any confusion that may arise from not knowing.

Once you have everything installed, it's time to get your git setup. I had some troubles here, and I'll quickly go over them here.
Assuming you're following the steps [here](https://docs.docker.com/opensource/project/set-up-git/), everything worked for me up until 
**Task 3, Step 10** where you are asked to push the changes you made back to GitHub.

Here's what happened at that stage for me:

``Nicks-iMac:docker-fork nickshields$ git push --set-upstream origin dry-run-test
Username for 'https://github.com': nickshields
Password for 'https://nickshields@github.com': 
remote: Permission to moxiegirl/docker.git denied to nickshields.
fatal: unable to access 'https://github.com/moxiegirl/docker.git/': The requested URL returned error: 403``

The solution, which was found [here](http://stackoverflow.com/questions/7438313/pushing-to-git-returning-error-code-403-fatal-http-request-failed), was to do the following:
1. Edit `.git/config`
2. Find `url=` entry under section `[remote "origin"]`
3. Ensure that the address specified is of this form: `https://github.com/YOUR_USERNAME/docker.git`
   where YOUR_USERNAME is your GitHub username.
   




