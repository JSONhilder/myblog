---
title: "Using ngrok With Hugo"
date: "2019-08-04"
draft: false
image: "imgs/blog-3.png"
description: 
tags: ["Hugo", "Web Dev"]
type: "post"
---

## Prerequisites

- Hugo 
- Hugo project ready for testing on a localhost
- ngrok
( download: https://dashboard.ngrok.com/get-started )

## What is ngrok

ngrok is a nifty tool to use with applications, websites and a multitude of other projects, ngrok by its description:

> 
  ngrok allows you to expose a web server running on your local machine to the internet. Just tell ngrok what port your web       server is listening on.
  
Another cool thing to note with ngrok is its real time web UI on port 4040 (127.0.0.1:4040) where you can monitor your web traffic along with things like HTTP requests and their responses, configuration settings and alot of other metrics.

<a href="https://ngrok.com/" target="_blank"><img src="/imgs/ngrok-logo.png" width="200" ></a>

## How do we use our hugo site with ngrok

I discovered ngrok when looking into alternatives for local host testing with pwa's and thought it could be quite cool to use it when developing a hugo site in terms of its mobile look, since google dev tools works but to get the actual look feel on a physical device is always nicer in my opinion.

So to get it working we first have to create a session with ngrok by running this command in our terminal:

    ./ngrok http 1313

The reason to type 1313 because hugo by default uses port 1313 to run locally, if you are manually using a different port type the port you are using.

Then you will see a few things happen in the terminal, the session will be created and your account information as well as the url to the web interface and most importantly the forwarding addresses will be shown these forwarding addresses can be shared and accessed via any browser.

## Making them work together

Since we have created our session we can run hugo locally to be viewed on port 1313. There are a few things to do to make sure it all works correctly, 

**(I ran into issues here with the css style sheets etc not loading and returning an html5 page with no styling)** 

firstly we need to copy one of those forwarding addresses from the terminal either http or https ***but just the number letter combo*** with this we will change the base url of hugo when we start up a local session, in our command we also need to set appendPort to false( these will only run with the command and not change your sites normal configuration ). See the examples below:

Command to run a local host over riding the baseURL in the config file and making appendPort false:

    hugo server -anyOtherflags -b *generatedURL*.ngrok.io --appendPort=False
    
Example with real info and displaying drafts as an extra flag:

    hugo server -D -b 29da620e.ngrok.io --appendPort=False
    

Now if we were to navigate to a forwarding address in our terminal via our browser on our phone we can see the localhost.