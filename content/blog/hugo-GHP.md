---
title: "Deploy your Hugo site on Github Pages"
date: 2019-05-01T19:26:33+02:00
draft: False
image: "imgs/blog-1.png"
description: "A step by step guide on deploying your Hugo site"
tags: ["Hugo", "Web Dev"]
type: "post"
---

## Prerequisites

- git on your pc and a GitHub account
- github SSH key, here's a link to do so https://devmarketer.io/learn/set-ssh-key-github/
- Hugo project ready to deploy


Hugo is a nifty static site generator made to be very flexible and very fast, so much so that on their site they claim to be the **world's fastest framework** for building static websites! 

If you haven't heard of Hugo you definitely should click the gopher to check out the Hugo website and how to get started!

<a href="https://gohugo.io/" target="_blank">
<img src="/imgs/go-logo.svg" width="250" >
</a>

Heres a step by step guide to deploying your Hugo site to GitHub Pages, the coolest part is it's free and you will use your GitHub repo that holds all your Hugo files to host. 

This will allow you to make changes locally and then push them to the repo and make those changes live with a simple script, this is a slightly longer way as there is a way to do it using a continuous integration tool called Travis CI, that is the next blog I am busy with, so it should be up soon if you want to see that. 

---

## Creating The Needed Github Repos

The files you work with to create your Hugo site and the files that actually display the website are different, what serves(displays) the website resides in the public directory. You can see this happen if you run the command `Hugo` in your site directory it will create the public directory.

To make the whole process clear let's determine the folders we will work with:

- Your local Hugo site folder ( this is where you have been designing your site, containing layouts, content, etc)
  
The other two folders will come from the repo's we create.

- Create a repo for your Hugo site files, i.e MySite
        
        Remember to clone this repo so you have the folder on your computer:
        git clone git@github.com:gitUserName/MySite.git
    

- Create a repo for the public files that serve the website this will be gitUserName.github.io

        We do not need to clone this as we will create a submodule soon.


After those steps, you should have your local Hugo site folder as well as an empty folder **MySite** on your pc and an empty repo on GitHub called **gitUserName.github.io**

1. Local Hugo site folder on the computer
2. Empty Mysite folder on the computer
3. Empty YourGitUserName.github.io on GitHub

<br>

---

## Removing public folder and pushing Hugo files to GitHub

We now need to copy the contents of our local Hugo site folder into the new folder MySite, then in your terminal cd to this MySite directory and run your server for a final check that everything is how you'd like. 

Before we can push these changes we need to edit the config file and make the following change:

    baseURL = "HTTPS://YourGitUserName.github.io/"

Without this change, the site will not display.

Once happy cancel the server with `CTRL + C` and run the command:

    rm -rf public

This will remove the public folder in mySite, once this is done we can run our git commands to push these files.

    git add.
    git commit -m "Initial commit."
    git push origin master  

So we now have our MySite folder on GitHub with our Hugo site files inside of it. 
<br>
<br>
!-**Optional**-! We no longer need to use the local Hugo site file, so you can backup or get rid of the folder since we only need the MySite folder.

<br>

---

## Creating the submodule to our .github.io repo

So to recap we now have MySite folder with the contents of your Hugo site on your computer and gitUserName.github.io on GitHub which is an empty repo.

Our next step is to create a link between the two repo's, so when we open our MySite folder in the terminal and run the `Hugo` command to build our site it will build to the public folder (remember the one that serves the site) inside the gitUserName.github.io folder, we can do this with git submodules, here's how:

Navigate to your MySite file and in the terminal, run this command:

    git submodule add -b master git@github.com:<gitUSERNAME>/<gitUSERNAME>.github.io.git public

This can be a bit confusing, but it will create a folder called public which basically is a folder linked to your gitUserName.github.io repo anything inside this folder will be in that repo. It should become more clear soon.

<br>

---

## Generating your Hugo site

Here is the final step, make sure you are in the MySite folder and in the terminal run the command:

    Hugo

This will generate the files that will serve our website, but it will generate them inside the .github.io folder.

If we run git status we will see:

    modified:   <USERNAME>github.io (untracked content)

Now inside the my blog folder we have to cd further into username.github.io and push those changes:

    cd <USERNAME>github.io
    git commit -m "Initial commit."
    git push origin master

After you push to the repo your site should be live on `https://USERNAME.github.io/` and that it! 

And the final step is to cd back to the myblog folder where we can push the changes to the development files

    cd ..
    git commit -m "your commit message"
    git push origin master

You have now created a folder to hold all your working files of the hugo site and another folder to actually server your website on GitHub for free!


# Final note

You will see at the end to push your changes is quite the run around, we can automate that task to make it alot less work using Travis CI which has a small setup required, [see my blog on how to set it up and get started using Travis CI](/blog/travisci/)