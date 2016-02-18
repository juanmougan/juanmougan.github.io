---
layout: post
title:  "Why I chose Rails for my web application"
date:   2015-03-02 16:13:00
categories: Development Ruby on Rails Sails.js MVC Opinion
---
On a [previous post](http://juanmougan.github.io/jekyll/update/2015/02/14/setting-up-angular-sails.html), I wrote about how to get up and running with a Sails.js project. The motivation for that particular arcticle was simple: I was exploring checking some frameworks to do a [smallish web application](https://github.com/juanmougan/backend/), and Sails had three interesting features:
- It was heavily inspired by Ruby on Rails, which I had breafily used before
- It was a JavaScript based framework, and it's a language I had (and I still have) to learn a lot better
- And also, another cool feature was it was really quick and easy to set up a REST API, which was one of my project's requirement. You can bootstrap a working API _really_ fast, in a painless way.

However, one of the main requirements I had, was to parse a CSV file having un-normalized data for Students, into  normalized object structure to be used by the system. To do so, I just started typing some Ruby code... because I love Ruby as much as I'm unfamiliar with JS. Eventually, the full [parser "prototype"](https://github.com/juanmougan/parseCsv) was ready... and it was the time to make a decision. Should I [stick with Sails](https://github.com/juanmougan/backendNotificaciones/) (which is based on node.js), and spawn a Ruby process to parse my CSV? Or should I rewrite my (at that point, really basic) APIs in Ruby?

I decided to go with a full Ruby solution, because I believed it would help manteniance and configuration, and I chose Rails because I had some experience using it. At least, I didn't have to scaffold everything, I knew how to make by hand a full controller, with its views and routes. The `CsvImporterController` was written that way, evntually I ended up using scaffold in some other parts, but it was a matter of lazyness ;)

At first, I didn't want to use Rails, because I didn't want to use a full stack framework. Since I needed to write both a frontend and an API, I believed that wouldn't be so useful. Besides, I didn't know how to serve both JSON and HTML from a Rails controller. I ended up writing two similar controllers for the "duplicated" entities, which didn't feel like an elegant solution. This is something I still need to research about, and refactor it when possible.

Anyway, which was the main reason why I decided to use Rails anyway? I believed (and I still do) that Rails was  an excellent tool to _bootstrap a project quickly_. What I coded first using Sails was no more than a prototype, an idea of what I would like my API to look like. Using Rails, I was able to create a _working prototype_ quite easily, and I was up and running really _fast_. It wasn't 100% painless, but it _works_. It should have a really better frontend, to have a better user experience, but it _works_. It should probably have some AngularJS, and less (if none) ERB... _but it works_.

Anyway, today I came across [this post called "Where and why I'm still using Rails"](http://blog.arkency.com/2016/02/where-and-why-im-still-using-rails/) which lead my to [this other post](http://blog.arkency.com/2016/02/rails-mvp-vs-prototype/) by the same author. I believe it was a really valid criticism on Rails, specially for ActiveRecord, but I also think it makes a great point: Rails will allow yo to do something bigger than just a "working prototype", as I thought last year. It will allow you to build a _production ready web application_, if you are willing to deal with its caveats. And I guess that was the reason I decided to use it to build my app — because I knew it would be a full solution.

I'm about to start a new pèrsonal project with some friends, and we're still deciding the technology stack. One of them is a big Scala fan, so it would probably be Play Framework. I hope that would give me some new cool stuff to learn :)
