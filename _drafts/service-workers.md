---
title: Service Workers explained
sub_title: &shy; a primer on service workers
date: 2017-12-07 16:58:00 +0100
categories: blogging
tags: [pwa, app development, service workers, sw]
---

I've been hearing a lot about service workers for a couple of years now, but hadn't really figured out what the fuzz was about. To me the term "Service Worker" doesn't really ring any bells in it self, so it's been somewhat of an abstract concept to me. That is, until I read [this short explanation](https://developers.google.com/web/fundamentals/primers/service-workers/):

> Service worker is a programmable network proxy, allowing you to control how network requests from your page are handled.

Essentially meaning: **Service Worker => Proxy**

I don't know if this makes just as much sense to you, but bear with me as we dig further into this:

The **:one:st** time you visit a website (or a PWA) that registers a service worker not much happens: The service worker [registers, installs](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle) - probably precaches some assets - and then sits idle [waiting](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle#activate) for the following request(s).

The real [McCoy](https://en.wikipedia.org/wiki/The_real_McCoy) is when you visit the same website (or PWA) the **:two:nd time** - that is, after closing all browsers/tabs for the given site and re-opening it in a new tab/browser:  
_Note: In Service Worker mojo the 'same' website is called `scope`. This means you are visiting a page at the same level or deeper from where the SW was registered._

**Now** what happens is, the browser sees you're visiting a page that is now *controlled* by your service worker and therefore it will proxy requests through your service worker (by raising a `fetch` event) for all the assets it needs to render the page (html, css, js, img) - and yes, also assets _outside_ your current `scope` [CONFIRM!?].

If your service worker responds to the request through the `event.respondWith(...)` method then that asset will be used straight of the cache. If not, then the browser will request the resource _the usual way_: From the browser's own cache or from the server (your server or 3rd party).   