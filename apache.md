#Apache Notes

####Restarting the Server
    sudo apachectl -k restart

##Fixing CORS Issues
**Cross-domain AJAX** Turn on CORS in the `.htaccess`

    # Enable cross-origin AJAX requests.
    <IfModule mod_headers.c>
        Header set Access-Control-Allow-Origin "*"
    </IfModule>

####More Information

(http://code.google.com/p/html5security/wiki/CrossOriginRequestSecurity)

(http://enable-cors.org/)

##PHP5.5 Installation via HomeBrew

Main Configuration File: 

    /etc/apache2/httpd.conf

Virtual Hosts Setup

    /etc/apache2/extra/httpd-vhosts.conf

To enable PHP in Apache add the following to httpd.conf and restart Apache:

    LoadModule php5_module    /usr/local/opt/php55/libexec/apache2/libphp5.so

✩✩✩✩ Extensions ✩✩✩✩

If you are having issues with custom extension compiling, ensure that
you are using the brew version, by placing /usr/local/bin before /usr/sbin in your PATH:

      PATH="/usr/local/bin:$PATH"

PHP55 Extensions will always be compiled against this PHP. Please install them
using --without-homebrew-php to enable compiling against system PHP.

