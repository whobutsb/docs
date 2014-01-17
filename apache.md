#Apache Notes


##Fixing CORS Issues
**Cross-domain AJAX** Turn on CORS in the `.htaccess`

    # Enable cross-origin AJAX requests.
    <IfModule mod_headers.c>
        Header set Access-Control-Allow-Origin "*"
    </IfModule>

####More Information

(http://code.google.com/p/html5security/wiki/CrossOriginRequestSecurity)

(http://enable-cors.org/)

