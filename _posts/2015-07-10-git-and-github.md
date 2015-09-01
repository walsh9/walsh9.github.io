---
layout: post
title:  "Version control with git and GitHub"
date:   2015-07-10 09:00:00
categories: "programming"
---

This week at Dev Bootcamp, I learned about version control using git and GitHub. Well, I've used git and GitHub for a while on my own, but the curriculum really helped me to soldify some concepts.

So what's version control? At its most basic, version control is keeping track of old versions of files. For example, a very primitive form of version control is keeping files named `document rev 1.txt`, `document rev 2.txt`, `document rev 3.txt`, etc. This is not recommended.

Git is a more sophisticated version control system. It's a computer program that can track changes for whole sets of files. A set of files tracked with git is called a repository (it's like a folder). When you make changes to files in a repository, your new revision is saved in something called a 'commit'. Each commit stores the current state of the files, a timestamp, the name of the person who made the changes, and a short message written by the committer.

If you manage your software source code with git you can go through the history of commits to see all sorts of useful information. Find out when a specific feature was introduced. Find out who added a certain line of code so you can ask them about it. Build all your old versions until you find the last version that didn't have the pesky bug you just discovered. And more.

One of the interesting features of git is that it's a _distributed_ version control system. This means you can keep multiple copies of a repository on different computer systems. For example you can have one copy of your repository saved up on the internet, where it can be accessed from anywhere. That's actually what GitHub does.

GitHub is a service that will let you host your git repositories on their servers. For open source projects with many contributors, this is very useful. The primary repository is hosted on GitHub, and contributors can 'clone' the repository to their local computer to make changes. When contributors are done with their modifications, they can post their commits and the maintainers of a project can decide whether or not to accept each change. Git and GitHub both provide features that make coordinating projects like this easier.

## P.S.

I didn't really talk about branches above, but when I read the curriculum about pushing changes I was taken aback by this section.

> "Now it's time to make your changes live on GitHub. There are two ways to do this, but we aren't going to cover the easiest one because it's bad practice and we've had feedback from students that it should not be included in the curriculum."
> 
> "The best practice way is by making feature branches and pull requests, which is highly favored when working with teams. We recommend using this process, because you will not be happy with yourself if you push to master at Dev Bootcamp."

Anyway, I know this bad practice well and have done it all the time on my own projects. Oops. I think I have a ways to go when it comes to working with teams. But that's why I'm here.
