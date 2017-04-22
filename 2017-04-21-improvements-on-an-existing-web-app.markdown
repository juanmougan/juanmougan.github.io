---
layout: post
title:  "Getting started with Backup gem"
date:   2016-09-05 16:15:00
categories: Development
---
Today I was wondering about one of the parts of my college's final assignment:
[the backend module](https://github.com/juanmougan/backend), a Ruby on Rails fullstack web app.  
Since it was a college assignment, I put most of the effort in the functional
requirements, which led to the presence of some amount of [technical debt](https://en.wikipedia.org/wiki/Technical_debt) in the final
solution. This, of course, is undesirable, and should be reduced as possible.  
This is the list of possible improvements I came across:

- The first is the most obvious: since the application serves both [regular HTML](https://github.com/juanmougan/backend/tree/master/app/controllers) and also acts
as a [REST API](https://github.com/juanmougan/backend/tree/master/app/controllers/api/v1), there's some code duplication in the controllers. When I coded this, I googled a little about how to reduce it, but I ended up doing this naive approach.  
Of course, an intelligent approach would be to separate the API, and create a
brand new project for the frontend. Say, node.js serving some HTML and your
favourite JS framework (or vanilla JS), and a pure API served by another Rails
server.  
This looked like the obvious way to code a system like this in 2015 and later, so
why didn't I do this? Well, again, functional vs non functional requirements:
back then, I had some experience using fullstack frameworks (Rails in particular),
but zero experience using a frontend-only stack (like, Angular). So, I decided
to save some time, and do some code duplication.

- The second obvious aspect to reduce the technical debt would be to add a suite of
automated tests. I'm planning to use this app as a playground to practice some
Ruby's test frameworks, so I might add some stuff here in the future.

- One not so obvious improvment can be made in the jobs section. In particular,
let's talk about the [CsvImporter](https://github.com/juanmougan/backend/blob/master/app/jobs/csv_importer_job.rb) job.  
While testing the app, I realized that inserting some amount of data, like 100k
rows, would take a lot of time. Checking the logs, the problem was evident: the
app was creating N transactions, and if N was really big (like 100k), it caused
a big delay when importing all the rows. That was easy to fix, [wrapping the
inserts in a single transaction](https://github.com/juanmougan/backend/blob/master/app/jobs/csv_importer_job.rb#L138).  
However, what if N becomes even bigger, say 1M rows? Can the database handle such
a big transaction?  
One possible solution to this could be to use an
[asynchronous approach to handle long running jobs](http://farazdagi.com/blog/2014/rest-long-running-jobs/),
to make sure we're not blocking the client for a long time. Of course, the feasibility
of this would depend on the size of N.

- Related to both previous items, running some performance/stress tests would be
useful to determinate if the synchronous approach is good enough, or if we need to
go for an asynchronous solution. A framework like
[JMeter](https://blog.flood.io/load-testing-a-restful-api-with-ruby-jmeter/)
would be useful to run these tests.

- Finally, the version of the [GCM gem I used](https://github.com/spacialdb/gcm)
doesn't handle sending messages to more than 1000 recipients at a time, which
could be a problem if this is a valid use case.

That's it for now, see you next time!
