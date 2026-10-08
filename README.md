# via

my self-hosted simplified version of ngrok (the first one)

basically it allows me to put web services on my laptop out on the internet for
testing (particularly useful for testing OIDC claims/webhook-type stuff)

on the client side it needs:

- [wstunnel](https://github.com/erebe/wstunnel) — the tunnel itself
- [caddy](https://caddyserver.com/) — runs locally too, to put basic auth in
  front of whatever port i'm exposing (see below)
- [rbw](https://github.com/doy/rbw) — unlocked, to pull the mTLS cert/key out of
  bitwarden. `VIA_CERT`/`VIA_KEY` in the env skip this

## auth

a slot is a public URL, so by default nothing hits my local port unauthenticated:
wstunnel dials a local caddy that demands basic auth and forwards on. `VIA_PASS`
is required (no random generation); user defaults to `$USER`.

- `VIA_PASS=hunter2 via 3000` serves behind basic auth
- `VIA_USER=me VIA_PASS=hunter2 via 3000` changes the username
- `VIA_NOAUTH=1 via 3000` exposes the port raw

this repo's more of a "how i'm doing it", and this seemed to be better than
using a github gist for some reason

## server config

requires a publicly accessible server to run all the server side goodies

another [caddy](https://caddyserver.com/) does TLS termination for these
endpoints, and [wstunnel](https://github.com/erebe/wstunnel) server does the
listening and redirecting
