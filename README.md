#Cheat Sheets and Documentation
Documentation and Information about programming, server management, web server management, and other frequently searched for documentation.

Inspired by [Tyler Cipriani](https://github.com/thcipriani/)

###[Apache Docs](apache.md)
###[MySQL Docs](mysql.md)
###[PHP Docs](php.md)
###[Vagrant](vagrant.md)

##Networking 
__Helpful Links__
- http://nerderati.com/2011/03/simplify-your-life-with-an-ssh-config-file/
- http://aarvik.dk/ssh-fundamentals-cssh-and-fabric/

###SSH
Your SSH configuration file lives in `~/.ssh/config`

####File Defaults
    
    Host name
        User username
        HostName hostname
        IdentityFile /path/to/file
        Post port_number

####Port Forwarding
Forwards all local port 9906 to port 3306 on the remote host.
For example allows connecting to mysql db on gui using the localhost (127.0.0.1:9906).

        Host name
            HostName hostname
            User username
            LocalForward 9906 127.0.0.1:3306

##General Tips

####Background a Process
    ctrl+z
    fg //foregrounds the project
    jobs //shows running 
    fg %[num] //opens the job you want 

####Monitor the Output of a file 
    tail -f [/path/to/file]

####Renaming/moving files with suffixes quickly:
    cp /home/foo/realllylongname.cpp{,-old}

####Copy the working directory or file to the system clipboard
    //Copy the working directory
    pwd | pbcopy
    //Paste the clipboard
    pbpaste

####Start a tunnel from some machine's port to your local port 2001
    ssh -N -L 2001:localhost:80 somemachine

####Get external IP Address   
    curl ifconfig.me/ip -> IP Adress
    curl ifconfig.me/host -> Remote Host
    curl ifconfig.me/ua ->User Agent
    curl ifconfig.me/port -> Port
    thonks to http://ifconfig.me/

####Copy a file from the remote host to the localhost
    scp hostname:file_name /path/to/local/direcotry

####Copy a directory from the remote to the local
    scp -r hostname:file_name /path/to/local/directory

    
##Searching

**Find**

- Find stuff in the Filesystem Heirarchy
- Usually located at /usr/bin/find
- Searches recursivly below specified search path
- more info and examples: man find

```Shell
find <search_path> [options]
```

_Command Examples:_

- Find a file name 'cats.txt' below current directory

  ```Shell
  find . -name 'cats.txt'
  ```

- Find all files below current directory

  ```Shell
  find . -type f
  ```

- Find all directories below current directory

  ```Shell
  find . -type d`
  ```

- .txt files

  ```Shell
  find . -type f -name "*.txt"
  ```

- case insensitive file name

  ```Shell
  find . -iname "nOtSuReOfCaSiNg.txt"
  ```

- join find options with `-and` ex: find php files that start with cat

  ```Shell
  find . -iname "*.php" -and -iname "cat*"
  ```

- txt files recursively to a depth of 2 

  ```Shell
  find . -maxdepth 2 -type f -name "*.txt"
  ```

- Exclude files with `-not` ex: find all NON-text files

  ```Shell
  find . -not -name "*.txt"
  ```

- Files modified less than a day ago

  ```Shell
  find . -type f -mtime -1
  ```

- Directories modified more than 10 days ago

  ```Shell
  find . -type d -mtime +10
  ```

- All Files greater than 100 MB

  ```Shell
  find . -type f -size +100M
  ```

- All files smaller than 10 KB

  ```Shell
  find . -type f -size -10K
  ```

- Remove all zip files bigger than 100MB

  ```Shell
  find . -name "*.zip" -size +100M -exec rm -i "{}" \;
  ```

- Remove all files in /tmp older than 2 days

  ```Shell
  find /tmp -maxdepth 1 -type f -mtime +2 -exec rm -i "{}" \;
  ```

- Create a `.gitkeep` file in all empty directories:

  ```Shell
  find . -type d -empty -print0 | xargs -0 -I{} touch {}/.gitkeep
  ```


**Grep**

- Grep (g/re/p) stands for global regular-expression print. Its name is
  derived from a command in "ed" a Unix line-editor built in 1971.
- use flag i for case insensitve search
- use flag v to negate
- use flag P to use Perl-Compatible Regular Expressions (still "Highly Experimental" ::eye-roll::)
- use flag c to count matches (or pipe to wc -l [word-count lines - see man wc for details])

_Grep Examples:_

- Find out if Apache is running
  - On CentOS                                                            <br> `ps aux | grep -i httpd`
  - On Debian                                                            <br> `ps aux | grep -i apache`
- Find out how many instances of ffmpeg are running (wc -l counts lines) <br> `ps aux | grep -i ffmpeg | grep -v grep | wc -l`
- Find text 'get_user' in all files below current dir with line numbers  <br> `grep -HiERn 'get_user' .`
- Same as above, don't include .svn directory                            <br> `grep -HiERn 'get_user' . | grep -v '.svn'`
- How many proccessors does a system have                                <br> `grep -c CPU /proc/cpuinfo`
- Same as above                                                          <br> `cat /proc/cpuinfo | grep -i cpu    | wc -l`
- Same as above                                                          <br> `grep -i cpu /proc/cpuinfo | wc -l`
- How many users are on a system besides you?                            <br> `grep -cv `whoami` /etc/passwd`
- Same number as above + 1 (total system users)                          <br> `cat /etc/passwd | wc -l`
- What shell is dave using?                                              <br> `cat /etc/passwd | grep dave | cut -d: -f7`


**Ack**

- Ack searches files below the current directory
  recursively. It's ideal for use with code since
  it automatically excludes any .svn, .git or .cvs
  direcories from its search

- ack is not a gnu utility and therefore is not included by default on most
  unix-like systems. To install:
  on debian: apt-get install ack-grep
  on centos: yum install ack

_Ack Examples:_

- search for a pattern in all files recursively     <br> `ack <pattern>`
- search for a pattern recursively case-insensitive <br> `ack <pattern>`
- search php files for thing recursively            <br> `ack --php <pattern>`
- search all files except javascript files          <br> `ack --nojs <pattern>`