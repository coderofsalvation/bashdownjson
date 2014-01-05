bashdownjson
===========

portable/easy way of generating of jsonfeeds using commandline (piping) using 100% bash and bashdown templates

Usage
=====

    $ ./bashdownjson 
    
      Usage: 

        add:        echo '{"foo":"bar"}' | bashdownjson add your.json
        reset:      bashdownjson reset your.json
        print:      bashdownjson generate your.json [maxitems]

One doesnt have to be an Einstein to figure this makes it perfect for crontab, fifo/pipe's and *any* kind of applications..since its all bash :)

Example
=======

put this into your crontab to generate the feed hourly (feel free to modify) with always the latest 10 items:
    
    @hourly /path/to/bashdownjson print errors.json 10 > /var/www/foo/errors.json

now with tail(f) you can easily monitor some (log)files etc:

    tailf /some/application/log.txt | grep "ERROR" | while read line do; echo "{\"msg\":\"$line\"}"done | ./bashdownjson add errors.json

This is just a simple example but you'll get the point I guess :)

Requirements
============

* written in +/- 50 lines of bash, the ultimate swiss army knife 

Credits
=======

* [bash(down) template 'engine'](https://github.com/coderofsalvation/bashdown)

Todo
====
* bashdownjson automatically detect jsonstring or textstring upon 'add'
