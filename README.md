# via

my self-hosted simplified version of ngrok (the first one)

basically it allows me to put web services on my laptop out on the internet for
testing (particularly useful for testing OIDC claims/webhook-type stuff)

on the client side it needs:

- [rathole](https://github.com/rathole-org/rathole) — the tunnel itself
- [caddy](https://caddyserver.com/) — runs locally too, to put basic auth in
  front of whatever port i'm exposing (see below)
- [rbw](https://github.com/doy/rbw) — unlocked, to pull the token/pubkey out of
  bitwarden. `VIA_TOKEN`/`VIA_PUBKEY` in the env skip this
- curl and openssl, which macOS already has

this one's set up to pull my keys/tokens from bitwarden,
and otherwise pretty hard-coded to my personal remote setup

## auth

a slot is a public URL, so by default nothing hits my local port unauthenticated:
rathole dials a local caddy that demands basic auth and forwards on. `via` prints
a fresh random password each run alongside the URL.

- `VIA_NOAUTH=1 via 3000` exposes the port raw
- `VIA_USER=me VIA_PASS=hunter2 via 3000` pins the creds instead of randomizing

this repo's more of a "how i'm doing it", and this seemed to be better than
using a github gist for some reason

## server config

requires a publicly accessible server to run all the server side goodies

another [caddy](https://caddyserver.com/) does TLS termination for these
endpoints, and [rathole](https://github.com/rathole-org/rathole) server does the
listening and redirecting, while rathole and this script does the client side
stuff.

pretty low tech but so far, it get's the job done
