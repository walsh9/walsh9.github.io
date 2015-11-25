---
layout: post
title:  "Adventures in GitHub Pages"
categories: "notes"
---

So, I recently changed this site from a WordPress blog to a GitHub Pages-hosted Jekyll blog. Here's how it went. 

## Switching from Wordpress to Jekyll

Converting the handful of posts I had to markdown was pretty simple. I used the WordPress [Jekyll Exporter](https://wordpress.org/plugins/jekyll-exporter/) plugin and fixed all my image links by hand. I also set up a few redirects with [jekyll-redirect-from](https://github.com/jekyll/jekyll-redirect-from) for a few posts that had changed urls so they wouldn't break any links.

## Setting up a custom domain with GiHub Pages

After that, I had a working Jekyll blog in my GitHub user page repo, `walsh9.github.io`. I wanted this site to be at my `walsh9.net` domain. So I went to my domain name registrar and set up some DNS records according to [GitHub's instructions](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/). I added a CNAME file to my repo with `walsh9.net` in it.  And since I didn't want any subdomains like `www` or `blog`, I set up an A record to pointing to GitHub's servers.

This worked and my site was now showing up at `walsh9.net`. But now all my project pages were showing up there as well.  For example, `http://walsh9.github.io/super-micro-paint` was now redirecting to and showing up at `http://walsh9.net/super-micro-paint`. This was kind of cool and some people might like it, but I didn't necessarily want all my projects to be at my personal domain like this, and  with this setup I couldn't pick and choose. It was all or nothing.  Basically `walsh9.github.io`, and all the project folders under it were entirely moved to `walsh9.net`.

## Switching from a user page to a project page

Luckily, this was easy enough to fix.  I renamed the repo from `walsh9.github.io` to `walsh9.net`. Now it was just a regular project repo. (By the way, the repo name could have been anything else. It didn't have to be `walsh9.net`. What's important is the CNAME file in the repo.) Oh, I also had to remember to create a `gh-pages` branch. The `[username].github.io` repo is special and will create pages from the `master` branch, but normal project repos need a `gh-pages` branch. Once I got that sorted, my page was showing up at `walsh9.net` again, but now my projects were back at their familiar `walsh9.github.io/[repo-name]` homes.

## Moving to CloudFlare

I thought I was done at this point. But then I tried to open `https://walsh9.net`.  It didn't load. Okay. After some research, I found out that using **HTTPS** with GitHub Pages on a custom domain with no subomain does not work well.  Next step was to [shift hosting to CloudFlare](https://www.benburwell.com/posts/configuring-cloudflare-universal-ssl/). After creating a free [CloudFlare](https://www.cloudflare.com/) account, and moving my DNS services over to CloudFlare I had working HTTPS, as well as a bunch of other neat features to play with.

## What about email?

Oh, since I'm now using CloudFlare for DNS I can't take advantage of my domain registrar's email forwarding...  I wasn't really using it anyway, but now that I couldn't have it I kind of wanted it. It's not fully set up yet but I've been playing around with using a free [Mailgun](https://www.mailgun.com/) account and setting up some rules to redirect to my email.  Seems like it might be a bit overkill but if it works it works.  I'm not actually fully sold on moving my main email address to my own domain yet so this part is just an experiment anyway.

## So...

I'm pretty happy with my new setup so far.  I know it's a little more dependent on external services now but I can always host a Jekyll-generated site anywhere so I'm not too worried.

## Update: 11/25/2015

Well, I guess during all that moving around something weird happened to all my gh-pages project pages because they were gone. I had to force GitHub to regenerate each site with this dirty trick:

```
git co gh-pages
git pull gh-pages
git commit -m 'rebuild pages' --allow-empty`
git push gh-pages
```
