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

I should make everyone aware that I am developing on a Mac (More specifically, a Hackintosh), to clear up any confusion that may arise from not knowing.

Once you have everything installed, it's time to get your git setup. I had some troubles here, and I'll quickly go over them here.
Assuming you're following the steps [here](https://docs.docker.com/opensource/project/set-up-git/), everything worked for me up until 
**Task 3, Step 10** where you are asked to push the changes you made back to GitHub.

Here's what happened when I tried to push to the remote:

`remote: Permission to moxiegirl/docker.git denied to nickshields.
fatal: unable to access 'https://github.com/moxiegirl/docker.git/': The requested URL returned error: 403`

The solution, which was found [here](http://stackoverflow.com/questions/7438313/pushing-to-git-returning-error-code-403-fatal-http-request-failed), was to do the following:
1. Edit `.git/config`
2. Find `url=` entry under section `[remote "origin"]`
3. Ensure that the address specified is of this form: `https://github.com/YOUR_USERNAME/docker.git`
   where YOUR_USERNAME is your GitHub username.
   
After making this fix, pushing worked fine.

The next problem I ran into was when I was trying to [Start a development container](https://docs.docker.com/opensource/project/set-up-dev-env/#task-1-remove-images-and-containers).
The step where you are asked to build the development environment using the command `make BIND_DIR=. shell` continously returned an error.
Initially, I thought the issue had to do with my internet connection timing out, but it actually had to do with how I had docker configured.
Docker defaults to running on 4 CPUs. Adjusting this to 1 and restarting docker solved this issue.
![_config.yml]({{ site.baseurl }}/images/fix.png)

Although I can't say why this is the case, I am almost certain that it has to do with the fact that I am running docker on a Hackintosh.
Nonetheless, I was able to successfully build after that. After the build succeeded, I went back and changed it to 4 cores, because I found
that it runs a lot faster that way (as it should, lol). Everything seems to be working as expected.

After following the subsequent steps, the next issue that arised was when I was instructed to edit the file `cli/command/container/attach.go`.
Funny enough, the file didn't even exist. Not in the container, not even on my local copy of the docker repo. But it did exist on my fork of the main codebase.
I'm not really sure why this happened, as I followed the steps as presented. I tried doing a `git pull`, but it didn't bring those lost files.
So I simply went back on GitHub and cloned my forked copy again and it brought the files back. I suppose in the future, it's important to ensure that 
when cloning a repository, that everything downloads correctly.

Other than that, I'm all setup. I have successfully completed the 'docker inception' technique. I looked over the test framework and it seems pretty straightforward.
I'm using docker as an excuse to learn golang and am pretty excited to tackle some entry level issues. I've already found some things in the documentation that could
be more clear or need to be updated, so that will likely my first contribution.

-Nick

