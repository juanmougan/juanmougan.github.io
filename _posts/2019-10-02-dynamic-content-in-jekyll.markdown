---
layout: post
title:  "Dynamic content in Jekyll and GitHub API's behaviour"
date:   2019-10-02 20:00:00
categories: Jekyll JavaScript Fetch
---

I added a very small dynamic section for this blog, that [queries GitHub's API](https://github.com/juanmougan/juanmougan.github.io/commit/f34faa11f5fbb2f260a715d696c13f6f6c52a737), to see my lastly updated project. It's a super simple usage of Fetch API, and some vanilla JS to 
update the HTML — nothing too fancy.  
However, today I discovered something curious. I had started a remote branch with some [commits on 09/30](https://github.com/juanmougan/spring-stuff/commit/83333fa4f32451b2d0f0d772fc6e6dc25d565817), but surprisingly, my component pointed [to some other project](https://github.com/juanmougan/estate-webscraper) I had worked on before. GitHub's [Repository page](https://github.com/juanmougan?tab=repositories) was correct, though.  
Added a [dummy commit](https://github.com/juanmougan/spring-stuff/commit/8d42b5e9b498cbf6bc782eb2d17a4793c6090db6) on `master` confirmed what I suspected. Listing [public repositories](https://developer.github.com/v3/repos/#list-user-repositories) by `updated` doesn't consider changes in 
other branches than `master`, you need to use `pushed` if you want to track all branches. This [same post](https://github.com/juanmougan/juanmougan.github.io/commit/9e3a9d3b594b2a8dd7d153fdc50fe9e1d76bdd79) served as Guinea pig to test this :)  
Anyway, it's a simple and cool way to keep track of your current work, and I'll use it as a minimalistic showcase.  
Thanks for reading!
