---
layout: post
title:  "Creating an API with fez, Kemal and Crystal"
date:   2017-09-18 23:00:00
categories: Crystal
---

This is a very basic example on using [fez](https://github.com/jwoertink/fez) to generate a [Kemal](https://github.com/kemalcr/kemal) API, running on [Crystal](https://crystal-lang.org)

1. Install Crystal
    
        $ brew install crystal-lang --with-llvm

    Using `--with-llvm` can be added to participate in the language development.

2. Clone fez to use it as a generator

	    $ git clone git@github.com:jwoertink/fez.git
	    $ cd fez/
	    $ make

    You can also use homebrew to install fez.

3. Create a sample API

        $ bin/fez crystal_kemal_api -t api -d ~/dev/crystal

    Will create an API in `~/dev/crystal`

4. Your app will have 2 primary dependencies to run.

	- Ruby
	- Crystal

    If you have those two installed, then your next step is to cd in to your new app's directory and run make install.

        $ cd crystal_kemal_api
        $ make install

5. To run the app, you can either:

	- `make run` - This compiles your assets in to their natural form, and then boots kemal.
	- `guard` - This will boot your kemal and then watch for any changes to the files.

    Both of these options will boot a server on `localhost:3001`. The difference is that using guard allows you to do live-reloading.

    An output example of running make run:

        $ make run
        crystal app.cr
        [development] Kemal is ready to lead at http://0.0.0.0:3001

6. Let's make the "controller" (on `src/crystal_kemal_api.cr`) slightly more interesting

        api("v1") do
          # /v1/test.json
          get "/health" do |env|
            {"message" => "Welcome to Kemal running on Crystal :)"}.to_json
          end
        end

7. Re-run and check the output

        $ curl 'localhost:3001/v1/health.json' | jq .

    Should return

	    {
	      "message": "Welcome to Kemal running on Crystal :)"
	    }

Enjoy! ;)
