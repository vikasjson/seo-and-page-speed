# seo-and-page-speed

 ### create .htaccess file for page speed and cache-control and other configurations
```
<IfModule mod_deflate.c>
  # Compress HTML, CSS, JavaScript, Text, XML and fonts
  AddOutputFilterByType DEFLATE application/javascript
  AddOutputFilterByType DEFLATE application/rss+xml
  AddOutputFilterByType DEFLATE application/vnd.ms-fontobject
  AddOutputFilterByType DEFLATE application/x-font
  AddOutputFilterByType DEFLATE application/x-font-opentype
  AddOutputFilterByType DEFLATE application/x-font-otf
  AddOutputFilterByType DEFLATE application/x-font-truetype
  AddOutputFilterByType DEFLATE application/x-font-ttf
  AddOutputFilterByType DEFLATE application/x-javascript
  AddOutputFilterByType DEFLATE application/xhtml+xml
  AddOutputFilterByType DEFLATE application/xml
  AddOutputFilterByType DEFLATE font/opentype
  AddOutputFilterByType DEFLATE font/otf
  AddOutputFilterByType DEFLATE font/ttf
  AddOutputFilterByType DEFLATE image/svg+xml
  AddOutputFilterByType DEFLATE image/x-icon
  AddOutputFilterByType DEFLATE text/css
  AddOutputFilterByType DEFLATE text/html
  AddOutputFilterByType DEFLATE text/javascript
  AddOutputFilterByType DEFLATE text/plain
  AddOutputFilterByType DEFLATE text/xml

  # Remove browser bugs (only needed for really old browsers)
  BrowserMatch ^Mozilla/4 gzip-only-text/html
  BrowserMatch ^Mozilla/4\.0[678] no-gzip
  BrowserMatch \bMSIE !no-gzip !gzip-only-text/html
  Header append Vary User-Agent
</IfModule>

##Tweaks##
Header set X-Frame-Options SAMEORIGIN

## EXPIRES CACHING ##
<IfModule mod_expires.c>
ExpiresActive On
ExpiresByType image/jpg "access 1 year"
ExpiresByType image/jpeg "access 1 year"
ExpiresByType image/gif "access 1 year"
ExpiresByType image/png "access 1 year"
ExpiresByType text/css "access 1 month"
ExpiresByType text/html "access 1 month"
ExpiresByType application/pdf "access 1 month"
ExpiresByType text/x-javascript "access 1 month"
ExpiresByType application/x-shockwave-flash "access 1 month"
ExpiresByType image/x-icon "access 1 year"
ExpiresDefault "access 1 month"
</IfModule>
## EXPIRES CACHING ##

<IfModule mod_headers.c>
    Header set Connection keep-alive
    <filesmatch "\.(ico|flv|gif|swf|eot|woff|otf|ttf|svg)$">
        Header set Cache-Control "max-age=2592000, public"
    </filesmatch>
    <filesmatch "\.(jpg|jpeg|png)$">
        Header set Cache-Control "max-age=1209600, public"
    </filesmatch>
    # css and js should use private for proxy caching https://developers.google.com/speed/docs/best-practices/caching#LeverageProxyCaching
    <filesmatch "\.(css)$">
        Header set Cache-Control "max-age=31536000, private"
    </filesmatch>
    <filesmatch "\.(js)$">
        Header set Cache-Control "max-age=1209600, private"
    </filesmatch>
    <filesMatch "\.(x?html?|php)$">
        Header set Cache-Control "max-age=600, private, must-revalidate"
      </filesMatch>
</IfModule>
```
