---
title: "Django Pythonanywhere"
date: "2019-08-05"
draft: true
image: "imgs/blog-4.png"
description: "How to host a Django project on Pythonanywhere."
tags: ["Django", "Web Dev", "Python"]
type: "post"
---
## Prerequisites

- Github account 
- Github repo holding Django project
- Django Project + basic understanding of Django
- Pythonanywhere account
- Being familiar with the linux terminal will help but not needed.

# Deploying a Django Project

There are quite a few choices when trying to decide where to deploy/host your Django projects, <a href="https://www.heroku.com" target="_blank">**Heroku**</a>, <a href="https://aws.amazon.com/ec2/" target="_blank">**AWS EC2**</a>, <a href="https://www.linode.com/" target="_blank">**Linode**</a>, the list can go on but in this case I decided to use <a href="https://www.pythonanywhere.com/" target="_blank">**Pythonanywhere**</a> it's a virtual machine loaded with a full python environment already installed, where you can develope and host websites, code etc. Out of those four options above this is most likely the easiest and fastest to get up and running, I am planning on writing blogs to deploy on Heroku and AWS EC2 instances in the future.

<img src="/imgs/pythonanywhere-white.png" width="400" >

So if you dont already have one, create an account with <a href="https://www.pythonanywhere.com/pricing/" target="_blank">**Pythonanywhere**</a> now if you want to follow this blog, it is completely free using the beginner account which is more than capable to host a small scale Django app!

Since this is on <a href="https://www.djangoproject.com" target="_blank">**Django**</a> it would be useful to have a basic understanding of Django. As this guide changes some file system settings, route paths and directorys of the project  and if you do not know what those are it will be confusing.

# Create The Database

First things first lets setup the database we will link to our django project on the Pythonanywhere dashboard. Navigate to the top right corner of the screen where the navbar shows Databases. We can choose between MySQL or Postgres, for my Django project I will be using MySQL so create a password and make sure its different to your Pythonanywhere account password! This will intialize a Mysql Database on your virtual machine.

Once completed it will give you a summary of your database details like host, username make sure to remember your password, which we will use later in our project settings! Also if you are wanting to run MySQL commands in the CLI in our summary of details there is an option:

    "Click a database's name to start a MySQL console logged in to it."

Lets click on the above so that we can create a new database specifically for our project, name it relevant to your project.

Thats it! We now have our database installed on our virtual machine ready to link to our project but first we need to get our project up and running.

One last note with this is that since we are using a free account we are limited to only 2 shells, so make sure to close `exit()` them correctly

We can now navigate back to our dashboard.

# Clone project to Pythonanywhere

Since Pythonanywhere is a virtual machine(**VM**) we can now clone our Django project from github into our VM.

Click on the button labeled "$ Bash" to open your VM's terminal, from here we can copy the URL of our github repository that holds our Django Project and clone it to the home directory, git is pre-installed so we just have to do:

    git clone "https://github.com/YourGitUsernam/YourGitRepoName"

We can now create a virtual environment for our django project, if you have used virtual environments before you may be familiar with pythons pipenv or virtualenv, however with Pythonanywhere it uses makevirtual environment so the command to create our virtual environment is:

    mkvirtualenv --python=/usr/bin/python3.7 myenv

We have to specify the Python version then the name of the environment as seen above, Pythonanywhere supports quite most Python versions but to be sure yours is check the docs.

Once installed it will automatically enter your environment your terminal should look something similar to this:

    (myenv) 20:26 ~ $ 

We can now go ahead and install Django within our virtual environment with pip!

    pip install django

The next step is situational, if you have any requirements.txt files we can now install them with pip as well.

    cd django_Project_folder
    pip install -r requirements.txt

Once all dependancies have been installed we can open our Pythonanywhere dashboard in a new tab don't close the terminal as we will use it again shortly.

So now we have our Database setup as well as django installed on our VM with all of its requirements installed, we can now move on to setting up our webapp to host our Django project.

# Creating A Web App

Now navigate to the Web link in the top right of the dashboard, and once the page loads click on the Add a new web app, since we have a free account we cannot have a unique domain name it will automatically be set to your **username.pythonanywhere.com**, click next.

The next slide will ask you to select a python webframe work, select the *"Manual configuration"* option and then your python version that you installed in the previous step.

After that just click next again and it will create the web app for you. You will now see a configuration page here we can set a lot o f parameters, directorys etc for our web app lets scroll down the page to the *virtualenv* section, here we will set our virtual environment we set up previously, in my case it was just myenv, type yours into the box and it will find the env with that name.

Next in the configuration page scroll to the code section and open  "WSGI configuration file" in a new window and remove everything besides django section it should look something like so: 

    # This file contains the WSGI configuration required to serve up your
    # web application at http:/username.pythonanywhere.com/
    # It works by setting the variable 'application' to a WSGI handler of some
    # description.
    #

    # +++++++++++ GENERAL DEBUGGING TIPS +++++++++++
    # getting imports and sys.path right can be fiddly!
    # We've tried to collect some general tips here:
    # https://help.pythonanywhere.com/pages/DebuggingImportError



    # Below are templates for Django and Flask.  You should update the file
    # appropriately for the web framework you're using, and then
    # click the 'Reload /yourdomain.com/' button on the 'Web' tab to make your site
    # live.


    # +++++++++++ DJANGO +++++++++++
    # To use your own django app use code like this:
    import os
    import sys

    ## assuming your django settings file is at '/home/username/mysite/mysite/settings.py'
    ## and your manage.py is is at '/home/username/mysite/manage.py'
    path = '/home/username/Django_App'
    if path not in sys.path:
        sys.path.append(path)

    os.environ['DJANGO_SETTINGS_MODULE'] = 'app.settings'

    ## then:
    from django.core.wsgi import get_wsgi_application
    application = get_wsgi_application()


Above I have removed all the single # tags under the django section. The double ## represent the comments, so best to leave them as comments.

