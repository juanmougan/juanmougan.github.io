---
layout: post
title:  "Parsing a TOML file in Go"
date:   2017-09-03 23:00:00
categories: golang
---
I wanted to load configuration data in a Go application, using something equivalent to Java's property files. 
After a little bit of googling, I came across [this StackOverflow's answer](https://stackoverflow.com/a/16491396/3923525), which suggests using [TOML](https://github.com/toml-lang/toml) for managing configuration.  
Using [BurntSushi's example](https://github.com/BurntSushi/toml/blob/master/_examples/example.go) for his parser, I created a simple Go program to parse a couple of properties —which is exactly was I was looking for.  
Here is a working example

Inside TOML file

    ClientSecret = "YOUR-API-CLIENT-SECRET"
    ApiAudience = "YOUR-AUTH0-API-AUDIENCE"
    Auth0Domain = "YOUR-AUTH0-DOMAIN"

And the Go program to parse it

    package main

    import (
      "fmt"
      "os"
      "github.com/BurntSushi/toml"
    )

    type Auth0Config struct {
      ClientSecret string
      ApiAudience string
      Auth0Domain string
    }

    func main() {
      var conf Auth0Config
      if _, err := toml.DecodeFile("auth0.toml", &conf); err != nil {
        fmt.Println(err)
        os.Exit(1)
      }
      fmt.Printf("ClientSecret: %s\n", conf.ClientSecret)
      fmt.Printf("ApiAudience: %s\n", conf.ApiAudience)
      fmt.Printf("Auth0Domain: %s\n", conf.Auth0Domain)
    }

Hope this is useful!
