## Clortho? ##

KLOR-tho

It's a distributed k/v with a goal of becoming a full-on Dynamo.

## What Do I Need To Know? ##

Term      | Definition
----------|-----------------------------------
Instance  | A running Clortho cluster
Database  | An organizational unit for buckets
Bucket    | An organizational unit for keys
Key       | A mnemonic for referencing a value

## How Do I Do It? ##

* Set up your config file (YAML).

    storage_directory: /path/to/whatever
    rest_port: some_port_number

* Run it

    nohup clortho -c /path/to/config

### Queries ###

As could probably be guessed from the REST port set in the config, Clortho
provides a RESTish HTTP (well, sorta) interface.

The URI scheme is http://server:port/DATABASE/BUCKET/KEY

To set a key, PUT it. To set the key "123" in the "randomnumbers" bucket in the
"stuff" database from the Clortho instance running on localhost port 9001,
you'll do something like the following:

    curl -X PUT http://localhost:9001/stuff/randomnumbers/123 \
      -H "Content-type: text/plain" \
      --data "This is some random stuff right here."

To get a key, GET it. If you want the value for key "123" in the "randomnumbers"
bucket in the "stuff" database from the Clortho instance running on localhost
port 9001, you'll do something like this:

    curl -H "Accept: text/plain" http://localhost:9001/stuff/randomnumbers/123

## How Does It Work? ##

Right now? Barely. Hell, I haven't even written much beyond basic database and
bucket handling.

It uses leveldb for actual storage. It's pretty nifty.
