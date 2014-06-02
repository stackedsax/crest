"Curl"REST API Command line client
==================================

A generic CLI to access any RESTful service with a little bit of configuration.
Think of it as something in between curl and proper CLI.

It has options similar to curl to fetch and provide request body. ``-d, -H`` and ``-d`` are
same as curl. ``-X`` is changed to ``-m``. Currently, the tool uses ``requests`` to send
HTTP requests. In future, it may just be wrapper on top of curl delegating all options to
curl.

With following `configuration <https://github.com/manishtomar/crest/blob/master/configs/raxid.py>`_ in ``~/.crest/raxid/config.py``::

   tokens_request = {
       "auth": {
           "passwordCredentials":{
               "username":"REPLACE_USERNAME",
               "password":"REPLACE_PASSWORD"
           }
       }
   }
   config = {
       "name": "raxid",
       "description": "Rackspace Identity Service",
       "uriprefix": "https://identity.api.rackspacecloud.com/v2.0",
       "headers": {
           "accept": "application/json",
           "content-type": "application/json"
       },
       "resources": {
           "tokens/?$": {
               "templates": {"default": tokens_request},
               "aliases": {
                   "username": "auth.passwordCredentials.username",
                   "password": "auth.passwordCredentials.password",
               },
               "help": "Authenticate via username/password"
           }
       }
   }

one can authenticate to `Rackspace Identity Service <http://docs.rackspace.com/auth/api/v2.0/auth-client-devguide/content/QuickStart-000.html>`_
and extract token using following command::

   crest -s raxid tokens -m post -t -r username=myuname -r password=mypwd -o access.token.id

For more details check `usage <https://github.com/manishtomar/crest/blob/master/usage.md>`_

Installation
------------
::

   pip install crest
   mkdir -p ~/.crest/generic_history  # for --history and --service to work

Thanks
------

Thanks to Rackspace for having a culture of hacking on side projects and allowing me to work on this, and having an
*excellent* `open source employee contribution policy <https://www.rackspace.com/blog/rackspaces-policy-on-contributing-to-open-source/>`_