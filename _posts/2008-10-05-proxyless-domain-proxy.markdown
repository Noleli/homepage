---
comments: true
date: 2008-10-05 11:46:01
slug: proxyless-domain-proxy
title: Proxyless Domain Proxy
wordpress_id: 72
categories:
- Information
- School
tags:
- .htaccess
- Apache
- host
- mod_rewrite
- PHP
- proxy
- server
---

## The Premise


I have a site for a school project that I'm hosting on a school server. I want to keep it hosted there for reliability/accountability reasons (i.e. if their servers go down on the day of a presentation it's their fault; if I use my discount host, it's my fault), but I'd like to use a custom domain.

Neither [school](http://projects.si.umich.edu/) nor [my host](http://www.dreamhost.com/r.cgi?332275) seem to allow proxies (`RewriteRule ^/~nliebman(.*)$ http://localchi\.com$1 [P] doesn't work`), so there had to be a different solution.


## The Solution


First I need to credit this to [pippo over at Dev Shed](http://forums.devshed.com/apache-development-15/rewrite-proxy-i-think-48832.html).

Rather than having Apache rewrite the school URL to my own URL, the trick is to have PHP do all the work, and simply rewrite the PHP file's URL (on my server) to show the filename from the school server.

On my server, I created the following PHP file, called getRemote.php:

    
    <?php
    readfile( "http://projects.si.umich.edu/~nliebman/".$_SERVER[ 'REQUEST_URI' ] );
    ?>


Then, I added this rule to my .htaccess:

    
    RewriteCond %{REQUEST_URI} !/getRemote.php [NC]
    RewriteRule ^(.*)$ /getRemote.php [L]


I didn't need to touch anything on the school server. I do take a performance hit since my server needs to get the content from the school server before serving it to me, but it's pretty light-weight stuff, so it's worth it for the pretty URL.
