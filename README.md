# Recline

A simple tool to help relaxing on your Couch.

It started as our attempt to strip away the basics of what a CouchApp is down
to what _we_ think it's _core_ is:

> You should get CouchDB to do as much work for you as possible.

How relaxing is that?

## Installation

Recline depends on `curl` and `jq`, so please install those first. Then, in
some preferred working directory:

 1. `git clone https://github.com/Firkintun/recline.git`
 1. `cp ./recline/recline /usr/local/bin` - This step may have to be run
 with `sudo`, but handle that with care.

## Usage

Currently, `recline` has no help information (it _was_ just an experiment, after
all). That said, `recline` takes one argument: a Bash script to run your
updates. From that script, `recline` expects a handful of variables and function
calls to be useful. An example is worth more than all the prose I could muster:

```
# Variables
## Where CouchDB is located.
HOST=localhost:5984
## The admin user name desired.
USER=admin
## The admin password desired.
PASS=password
## A small piece of boilerplate to be removed in the future.
ROOT=$USER:$PASS@$HOST

# Helpful, but not required: start verbose mode.
set -v

# Guarantee the admin user exists.
admin

# Guarantee a "locations" database exists.
database locations

# Run an update. The first argument is the full path to be PUT to, whereas the
# second argument is a runnable file whose output should be the JSON document
# to PUT. This example shows a Node script, but any script will do.
update locations/_design/validation data/couch/locations/validation.js

# Another example use case: seeding users.
update _users/org.couchdb.user:schoon data/couch/users/schoon.js
```

## Alternatives

There are several, full CouchApp implementations. That said, when you're just
looking for a little more muster around ACLs with a simple, JSON-only API,
they're too much.

If anyone knows of another tool to idempotently update Couch with some seed
data and design documents, we're all ears. Please don't hesitate to give us a
call.
