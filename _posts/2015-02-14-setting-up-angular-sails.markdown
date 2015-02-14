---
layout: post
title:  "Setting up a Sails.js + AngularJS project part 1"
date:   2015-02-14 13:17:28
categories: jekyll update
---
This is the first post in a series to set up an AngularJS UI, backed up by a Sails.js API.

### Setting up a Linux environment ###

### Setting up a Windows environment ###

1. First of all, node.js needs to be installed. To do so, download a msi package from [the node.js](http://nodejs.org/download/) website.

2. Clone the [Angular seed repository](https://github.com/angular/angular-seed), like this: 
`git clone https://github.com/angular/angular-seed.git`

3. Install Sails: `npm -g install sails`

4. Since running `sails lift` at this point failed, I installed the sails-disk component: 
`npm install sails-disk`

5. Lift the server: `sails lift`
