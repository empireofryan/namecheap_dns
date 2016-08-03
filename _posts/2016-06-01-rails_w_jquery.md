---
title: Rails with Jquery
excerpt: Filmr
priority: .7
categories:
  - works
background-image: rails.jpg
#date/lastupdated are optional
#date: 2016-06-01 18:29:51
#lastupdated: 2016-06-01 18:29:51
---
<h4>Filmr with Jquery</h4>
<a href="http://github.com/empireofryan/filmr">Launch Github</a>
<p>Filmr with Jquery takes the codebase from the prior Rails Filmr app and adds the functionality of JQuery to provide seamless AJAX page reloads.</p>

<p>The current iteration of the app includes a Devise authentication and Facebook Oauth Login. Create a new script, save by genre, and make comments on any script.</p>

<p>Take the following screenshot for example. The URL path, "localhost:3001/genres/3/scripts" refers to "genre: 3" which corresponds to the "Horror" scripts index page. Yet rather than following REST architecture and redirecting to the individual script page (i.e. "genres/3/scripts/51") the app loads a JSON template.</p>

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
