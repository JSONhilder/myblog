---
title: "TravisCI with Hugo"
date: "2019-07-28"
draft: False
image: "imgs/blog-2.png"
description: "How to use Continuous Integration with a Hugo website."
tags: ["Hugo", "Travis CI", "Continuous Integration"]
type: "post"
---
<img src="/imgs/travis-ci.png" width="300" >

# Travis CI, Github and Hugo

Travis CI is a continous Integration tool that can be used with GitHub projects, basically it allows us to test new code written for our GitHub repos before pushed changes get submitted.

This is a follow up/part 2 of my first blog, [Deploy your Hugo site on Github Pages](/blog/hugo-ghp/) which is a guide to hosting a Hugo website on GitHub Pages. You may want to read through and follow that before following this blog as it will help give the context more meaning.

Using Travis CI with your GitHub Pages website will allow you to create changes and push them to your repo as you would normally but then it will automatically test the changes and deploy the site with the new changes to your website! Cool right! 

# Setting up Travis CI Part 1

Travis CI will need to have write access to the site/repository, if you're following from the previous blog it would be, username.github.io, so that it can push the generated content to it.

Rather than giving Travis CI access to your personal GitHub account we can create a bot account on GitHub which is just a normal account but will be used to do all our Travis CI tasks, this way we can give this bot account access only to repositories that need to use Travis CI.

But to keep this post as simple as possible lets use our personal Github account.

Go to [Travis CI website](https://travis-ci.org/) and sign up for an account using GitHub.

Once signed up it will redirect you to your dashboard. In the top right corner you will see your profile navigate to the settings.

Here you will see all your public repositories, we will now create an environment variable to link Travis CI to the repo.Go to the settings page of the repository containing your hugo development files. 

Add an environmental variable named GITHUB_TOKEN and set the value to https://user:pass@github.com, using the credentials of your account.

Finally make sure that the *Display* value in build log switch is in the off position.

# Setting up Travis CI part 2

Travis CI can be set up to do specific tasks with a YAML configuration file. We can add a .travis.yml to our hugo site repository, this will cause the steps we define to take place once we push changes to the repository.

Our YAML file needs to execute three tasks for us:

* Install Hugo inside our CI virtual environment

* Call and Invoke the hugo command to build the site files

* Deploy the new website build files to username.github.io

This yaml file has a **build lifecycle** here is a [cheat sheet](https://devhints.io/travis) if you are interested, we will use:

* before_install

* install

* script

* deploy

At each of these steps we will tell travis CI to do certain things.

So now create a file and name it .travis.yml copy the content below into this file:


        sudo: required

        language: python

        git:
        submodules: false


        install:
        - sudo pip install pygments
        - wget https://github.com/gohugoio/hugo/releases/download/v0.31.1/hugo_0.31.1_Linux-64bit.deb
        - sudo dpkg -i hugo*.deb
        - rm -rf public || exit 0
        #removes (if there is one) old public directory 

        script:
        - hugo # This commands builds your website on travis

        deploy:
        local_dir: public 
        # Default static site output dir for Hugo
        repo: userName/userName.github.io 
        # This is the slug of the repo you want to deploy your site to
        target_branch: master 
        # GitHub pages branch to deploy to (in other cases it can be gh-pages)
        provider: pages
        skip_cleanup: true
        #required so that Travis doesn't remove the generated files before deploying.
        github_token: $GITHUB_TOKEN 
        # This is the authentication which setup in the travis-ci dashboard
        email: #github email
        name: #github UserName
        on:
            branch: master

All you need to do now is change the values of the file to fit your repo and github details and then push the file to the repo.

You can now visit your Travis CI dashboard to see your site building. If there is an error there is a log which you can troubleshoot from.

When CI has completed, your site should be live at https://username.github.io/.