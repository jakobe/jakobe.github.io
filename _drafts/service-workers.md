---
title:  The ins and out of registering a Service Worker
date:   2017-12-07 16:58:00 +0100
categories: blogging
tags: [pwa, app development, service workers, sw]
---

# Registering a service worker
I've been hearing about service workers for quite some time now, but it's been somewhat of an abstract concept to me. That is, until someone (link?) gave this explanation:

> Service Worker => Proxy

I don't know if this makes just as much sense to you, but bear with me as we dig further into this:

The **1st** time you visit a website (or PWA) that registers a service worker not much happens: The service worker registers, installs - probably precaches some assets - and then starts [waiting](link?)

The real <s>mccoy</s> is when you visit the same website (or PWA) the **2nd time** (that is, after closing all browsers/tabs for the given site and re-opening it in a new tab/browser):
**Note:** In SW mojo the **same** website is called `scope`. This means you are visiting a page at the same level or deeper from where the SW was registered.  
**Now** what happens is, the browser sees you're visiting a page that is now **controlled* by your service worker and therefore it will issue a `fetch` request to your service worker for all the assets it needs to render the page (html, css, js, img) - and yes, also assets _outside_ your current `scope` [CONFIRM!].

If your service worker responds with a ??? then that asset will be used straight of the cache. If not, then the browser will request the resource _the usual way_: From the browser's own cache or from the server (yours or from 