bashdownjson
===========

portable/easy way of generating of jsonfeeds using commandline (piping) using 100% bash and bashdown templates

Usage
=====

    $ ./bashdownjson 
    
      Usage: 

        add:        echo 'foo bar'       | bashdownjson add your.json
                    echo '{"foo":"bar"}' | bashdownjson add your.json

        reset:      bashdownjson reset your.json
        print:      bashdownjson generate your.json [maxitems]

One doesnt have to be an Einstein to figure this makes it perfect for crontab, fifo/pipe's and *any* kind of applications..since its all bash :)

Example
=======

put this into your crontab to generate the feed hourly (feel free to modify) with always the latest 10 items:
    
    @hourly /path/to/bashdownjson print errors.json 10 > /var/www/foo/errors.json

now with tail(f) you can easily monitor some (log)files etc:

    tailf /some/application/log.txt | grep "ERROR" | while read line do; echo "{\"msg\":\"$line\"}"done | ./bashdownjson add errors.json

Example output
==============

The 'add' command in the Usage-example above, would eventually generate this output when './bashdownjson print your.json' would be called:

    {    
      "system": "Linux lemon 2.6.32-042stab076.5 #1 SMP Mon Mar 18 20:41:34 MSK 2013 x86_64 GNU/Linux",
      "date": "Sun, 05 Jan 2014 16:56:49 +0100",
      "items": [
        {
          "id"  : "1388937285",
          "date": "Sun, 05 Jan 2014 16:54:45 +0100",
          "data": {"text":"foo bar"}
        }
        ,
        {
          "id"  : "1388937305",
          "date": "Sun, 05 Jan 2014 16:55:05 +0100",
          "data": {"flop":"flap"}
        }
      ]
    }


This is just a simple example but you'll get the point I guess :)

Requirements
============

* written in +/- 50 lines of bash, the ultimate swiss army knife 

Credits
=======

* [bash(down) template 'engine'](https://github.com/coderofsalvation/bashdown)
