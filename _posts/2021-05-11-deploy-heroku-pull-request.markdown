---
layout: post
title: "Deploying to Heroku on a pull request using GitHub Actions"
date: 2021-05-11 23:45:00
categories: GitHub Heroku
---

I came across this great [GitHub Action](https://github.com/marketplace/actions/deploy-to-heroku) to deploy to Heroku by
only doing a `git push` to your main branch. It's really simple to configure, but I wanted to be able to trigger a
deploy after a pull request gets merged as well.  
This turned out to be quite simple. Per Action's
[documentation](https://docs.github.com/en/actions/reference/events-that-trigger-workflows#example-using-multiple-events-with-activity-types-or-configuration),
by adding this snippet into the `yaml` file that describes the action:

```
on:
  # Trigger the workflow on push or pull request,
  # but only for the master branch
  push:
    branches:
      - master
  pull_request:
    branches:
      - master
```

<sub>I'm using the oldschool name for the mail branch 🤷‍♂️</sub>

Then, when a pull request is merged, the deploy gets triggered

![GitHub action](/assets/gh_action.png)

And the code gets deployed to Heroku

![Heroku Action](/assets/heroku_action.png)

Enjoy!
