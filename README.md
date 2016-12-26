#Download and Installation

`loklak` is free software, licensed with LGPL. To install `loklak`, you need JDK 1.8, git and ant. If you don't know what this is, then `loklak` is currently not something for you.

At this time, `loklak` is not provided in compiled form, you must build it yourself. It's not difficult and done in one minute!

***

###Download, Build, Run

The source code is hosted at https://github.com/loklak/loklak_server, you can download it and run `loklak` with:

    > git clone https://github.com/loklak/loklak_server.git
    > cd loklak_server
    > ant
    > bin/start.sh

After all server processes are running, loklak tries to open a browser page itself. If that does not happen, just open http://localhost:9000; if you made the installation on a headless or remote server, then replace 'localhost' with your server name.

To stop loklak, run: (this will block until the server has actually terminated)

    > bin/stop.sh

A self-upgrading process is available which must be triggered by a shell command. Just run:

    > bin/upgrade.sh
    
***

###Import A Message Dump

To import a message dump (which you get from the [dump directory](http://loklak.org/dump/) of every loklak peer), just move it to the `data/dump/import/` directory:

    loklak
        ⌊data
            ⌊dump
     
                ⌊import                                 // to import a dump, throw the dump in here, it will got to...
                ⌊imported                               // processed dump files from the import folder are moved here
                ⌊own                                    // dump files which this application creates, accessible at /dump/

Imported dumps are not deleted, but moved to the `imported` directory. Because extracted hashtags, links and user names are not part of the dump, this is done during the import process and written to the elasticsearch index. While imports are running, you can use the [/api/status.json](http://loklak.org/api.html#status) servlet to moniotor the import progress.

***

###Re-Build The Search Index

In case of application bugs, data structure changes or if you change your set-up for larger indexing shards, you can re-create the search index completely using the index dumps. To delete and re-create the index, do:

    stop loklak with bin/stop.sh
    delete the index folder at data/index
    move your dump files from data/dump/own/ to data/dump/import
    start loklak again - this will re-create the index folder
    the import starts automatically
    
***

###Use Kibana As Search Front-End


