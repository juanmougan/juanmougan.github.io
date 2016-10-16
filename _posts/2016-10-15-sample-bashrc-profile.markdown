---
layout: post
title:  "A sample .bashrc_profile for Mac OS, to run multiple JVMs"
date:   2016-10-10 22:00:00
categories: Configurations OSX
---

This is a sample `.bashrc_profile` file, to be used in any Mac OSX (or Linux, changing its paths) with bash shell. It allows you to run multiple JVMs with different versions at the same time. I have recopiled it from several Internet resources, and tailored it to my own needs.

	#export JAVA_6_HOME=$(/Library/Java/JavaVirtualMachines/1.6.0_65-b14-462.jdk/Contents/Home)
	export JAVA_6_HOME=/Library/Java/JavaVirtualMachines/1.6.0_65-b14-462.jdk/Contents/Home
	#export JAVA_7_HOME=$(/Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home/)
	export JAVA_7_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home/

	alias java6='export JAVA_HOME=$JAVA_6_HOME'
	alias java7='export JAVA_HOME=$JAVA_7_HOME'

	#default java7
	export JAVA_HOME=$JAVA_7_HOME

Of course, Java 8 could be added too. I hope you find it useful.
