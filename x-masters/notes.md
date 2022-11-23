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
