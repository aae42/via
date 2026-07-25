# via

my self-hosted simplified version of ngrok (the first one)

basically it allows me to put web services on my laptop out on the internet for
testing (particularly useful for testing OIDC claims/webhook-type stuff)

requires [rathole](https://github.com/rathole-org/rathole)

this one's set up to pull my keys/tokens from bitwarden,
and hard coded to my remote setup

this repo's more of a "how i'm doing it", and this seemed to be better than
using a github gist for some reason

## server config

requires a publicly accessible server to run all the server side goodies

[caddy](https://caddyserver.com/) does TLS termination for these endpoints,
and [rathole](https://github.com/rathole-org/rathole) server does all the
listening and redirecting, while rathole on the client does the client side
stuff.

pretty low tech but so far, it get's the job done
