---
comments: true
date: 2008-03-03 09:01:24
slug: a-subversion-gripe-htaccess-mod_rewrite-issue
title: A Subversion Gripe & .htaccess mod_rewrite Issue
wordpress_id: 7
categories:
- Information
- Site
tags:
- .htaccess
- mod_rewrite
- subversion
---

> EDIT: It turns out the fix below for the mod_rewrite issue does not work. I'd love to know why. If anybody knows, please either comment on this post or reply to [this thread](http://forums.applenova.com/showthread.php?t=28536). Thank you.


In starting this blog, I had to move my old website into a new branch of my `homepage` repository. I wanted to be able to do a server-side move from the root of the repository to a new subdirectory, like this:

    
    svn mv http://noahlieban.com/svn/homepage/* \
     http://noahliebman.com/svn/homepage/old-site/


Sadly, this didn't work. What did I have to do? Make the new directory (in the working directory or on the server; doesn't matter), then `svn mv` each file in one by one. Stupid. The reason is that it can't copy onto itself, which I guess is fair enough. The moral of the story is that a repository should always have a `/trunk` (or other root-level directory) _just in case_ it needs to be branched. Otherwise, it's a pain.

My second issue is not really a Subversion issue, but with the .htaccess file that Wordpress makes for its permalinks:

    
    # BEGIN WordPress
    <IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.php [L]
    </IfModule>
    # END WordPress


Now, I'm no expert in server configuration stuff, but this seems straightforward enough: If the requested file is neither a real file or real directory, do the rewrite rule. I don't actually care what the rewrite rule does, because my problem is that [Dreamhost](http://www.dreamhost.com/r.cgi?332275) sets up Subversion by making it accessible via http request at `http://domain.com/svn/repo/`, although `/svn/` is not a real directory in the root web directory on the server, so it gets caught by the second rewrite condition. This breaks Subversion over http.

I wanted to be able to add another condition that told it to only do the rule if the request URI does not start with `/svn/`, so I added

    
    RewriteCod %{REQUEST_URI}!^/svn/.*$


to the other two conditions. For some reason, this didn't work, though. I instead needed to add a new rule in the affirmative above the Wordpress one:

    
    RewriteCond %{REQUEST_URI} ^/svn/.*$
    RewriteRule ^(.*)$ - [L]


i.e. if it starts with `/svn/`, don't change anything. Why doesn't it work with an exception? I have no idea.
