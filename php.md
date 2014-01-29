#PHP Notes

###Configuration File
    /usr/local/etc/php/5.5/php.ini


##Pear Notes
If PEAR complains about permissions, 'fix' the default PEAR permissions and config:

    chmod -R ug+w /usr/local/Cellar/php55/5.5.8/lib/php
    pear config-set php_ini /usr/local/etc/php/5.5/php.ini

##PHP CLI
If you wish to swap the PHP you use on the command line, you should add the following to ~/.bashrc,
~/.zshrc, ~/.profile or your shell's equivalent configuration file:

      export PATH="$(brew --prefix josegonzalez/php/php55)/bin:$PATH"