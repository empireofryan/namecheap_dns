---
title: Angular Frontend on Rails
excerpt: Screenplay ranking app on AngularJS frontend with Rails API backend.
author: Ryan J
tags: featured
categories:
  - topics
background-image: angular.jpg
#date/lastupdated are optional
#date: 2016-06-06 12:56:46
#lastupdated: 2016-06-06 12:56:46
---
<h4>ScriptRank</h4>
<a href="http://github.com/empireofryan/scriptrank">Launch Github</a>
<p>ScriptRank is a reenvisioning of a prior Rails project. Now updated to Angular, the program functions as a single page app.</p>

<p>The current iteration of the app includes a Devise authentication, which only allows for a user to login and create a new script or browse and vote/review on already made ones.</p>

<p>The URL path, "localhost:3000/#/scripts" loads the scripts index page. What was previously done by routing into a "genres" URL. The magic of Angular filters searches the script based on clicking the genre.</p>

<img src="https://photos-6.dropbox.com/t/2/AAC6V_HsJB5Py0fY4dsLU50v3wdt9o8uu7mV5EVA4PmuPw/12/542197078/png/32x32/1/_/1/2/Screenshot%202016-06-02%2015.32.03.png/EMzIsasEGJ8CIAIoAg/vYfrnEc6JhLmrbzfvlI6Bx6xSt1nZF-IePDE8ht7dnc?size=2048x1536&size_mode=3" style="width:100%">

<p>Did you spot the link target at the bottom left? It points to a JSON object rather than a page. Check out the next image. Notice something about the URL? It's exactly the same!</p>

<img src="https://photos-3.dropbox.com/t/2/AABCgqkQKs6kMl6M5CAcYddGs3kThv4hoZ3x7bbpezF3tw/12/542197078/png/32x32/1/_/1/2/Screenshot%202016-06-02%2015.32.27.png/EMzIsasEGJ8CIAIoAg/HPgCn76HSDsZjSLXyEymLoe2kF1ps4uO6IW7oSi8CGA?size=2048x1536&size_mode=3" style="width:100%">

<p>You don't need to own a classic Thunderbird to want to take a look under the hood. Here's the magic behind the invisible reload functionality. Let's break it down step by step:</p>

<xmp>
def index
  @scripts = Script.where(genre_id: params[:genre_id])
    respond_to do |f|
    f.html { render :index }
    f.json { render json: @scripts }
   end
end

def show
  @script = Script.includes(:genre).find(params[:id])
  respond_to do |f|
    f.html { render :show }
    f.json { render json: @script }
  end
end
</xmp>
