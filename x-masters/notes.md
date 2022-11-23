I've just moved my site from wordpress to a static HTML site.

As you'd imagine, this move has caused a lot of broken links, so I am spending a lot of time reviewing the error log and addressing issues as they occur.

My error logs are starting to get a lot of new "AH00128: File does not exist"

But the errors are all strange, as there seems to be an "index.html" injected at odd places within the URL.

In the following example, note the "index.hml" after "presentations" and before "benefits"

/home/u736-x0ggcgpz79fo/www/maxdesign.com.au/public_html/presentations/index.htmlbenefits/

/home/u736-x0ggcgpz79fo/www/maxdesign.com.au/public_html/presentations/index.htmlliquid/example10.htm

As mentioned, there are LOTS of these.

Any suggestions as to what would be causing this and how to resolve?

## Old

#Rewrite to www
Options +FollowSymLinks
RewriteEngine on
RewriteCond %{HTTP_HOST} ^maxdesign.com.au[nc]
RewriteRule ^(.*)$ http://www.maxdesign.com.au/$1 [r=301,nc]


## New

#Rewrite to www
Options +FollowSymLinks
RewriteEngine On
RewriteCond %{HTTP_HOST} ^maxdesign.com.au [NC]
RewriteRule ^(.*)$ http://www.maxdesign.com.au [L,R=301]


## Suggested

#Rewrite to www
Options +FollowSymLinks




I've just moved my site from wordpress to a static HTML site.

As you'd imagine, this move has caused a lot of broken links, so I am spending a lot of time reviewing the error log and addressing issues as they occur.

I've just noticed a new, weird issue.

This works:

https://www.maxdesign.com.au/resources/index.html

This throws 500 - Internal Server Error

https://www.maxdesign.com.au/resources/

This is the same for all folders, including the root:

https://www.maxdesign.com.au/
https://www.maxdesign.com.au/workshops/
https://www.maxdesign.com.au/articles/
https://www.maxdesign.com.au/assets/
https://www.maxdesign.com.au/book/
https://www.maxdesign.com.au/contact-us/
https://www.maxdesign.com.au/css-layouts/
https://www.maxdesign.com.au/liquid/
https://www.maxdesign.com.au/presentations/
https://www.maxdesign.com.au/resources/
https://www.maxdesign.com.au/services/
https://www.maxdesign.com.au/training/

I can create a series of htaccess rules to manually fix this, but it seems odd that I'd need to?




I've just moved my site from wordpress to a static HTML site.

I've been creating a lot of rules in my maxdesign.com.au/public_html/.htaccess file

Most of these rules seem fine, but I'm noticing two isses:

ISSUE 1:

Any redirects from "articles" or "news" work fine:

Redirect 301 /articles/center/ /articles/center.html
Redirect 301 /news/center/ /articles/center.html

But any redirects from "presentation" do not work:

Redirect 301 /presentation/center/ /articles/center.html

Every instance where I redirect from "presentation" generates the following type of incorrect URL:

https://www.maxdesign.com.au/presentations/index.htmlcenter/

ISSUE 2:

Typing the following into the address bar:

https://www.maxdesign.com.au/book/

Generates this:

https://www.maxdesign.com.au/book/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/index.html/




Answe

 looked into it and I believe the issue with the /presentation/ redirects is caused due to the fact that there is a folder added inside the public_html folder with an index.html file inside .And the system is looking for /presentation/em inside it and causes a 404 error to occur. Could you please temporarily rename /presentation in the File Manager to /presentation1 for example, and we can test again 






