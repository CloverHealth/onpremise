# Sentry On-Premise Clover fork

Official bootstrap for running your own [Sentry](https://sentry.io/) with [Docker](https://www.docker.com/) and [GKE](https://cloud.google.com/kubernetes-engine/).

## Requirements

 * Docker 1.10.0+
 * Compose 1.6.0+ _(optional)_
 * GKE 1.7.8+ _(optional)_
 * [GCloud SDK]() 

## Up and Running with Docker Compose

Assuming you've just cloned this repository, the following steps
will get you up and running in no time!

There may need to be modifications to the included `docker-compose.yml` file to accommodate your needs or your environment. These instructions are a guideline for what you should generally do.

1. `mkdir -p data/{sentry,postgres}` - Make our local database and sentry config directories.
    This directory is bind-mounted with postgres so you don't lose state!
2. `docker-compose run --rm web config generate-secret-key` - Generate a secret key.
    Add it to `docker-compose.yml` in `base` as `SENTRY_SECRET_KEY`.
3. `docker-compose run --rm web upgrade` - Build the database.
    Use the interactive prompts to create a user account.
4. `docker-compose up -d` - Lift all services (detached/background mode).
5. Access your instance at `localhost:9000`!

Note that as long as you have your database bind-mounted, you should
be fine stopping and removing the containers without worry.

## Up and Running with Kubernetes

* git clone this repo
* cd into this repo's directory sentry_onpremise_kubernetes/
*  

```bash
kubectl -f create sentry/sentry.yaml
```

## Securing Sentry with SSL/TLS

If you'd like to protect your Sentry install with SSL/TLS, there are
fantastic SSL/TLS proxies like [HAProxy](http://www.haproxy.org/), [Nginx](http://nginx.org/)
and [Ingress-GCE](https://github.com/kubernetes/ingress-gce/blob/master/README.md#frontend-https).

## Resources

 * [Documentation](https://docs.sentry.io/server/installation/docker/)
 * [Bug Tracker](https://github.com/getsentry/onpremise)
 * [Forums](https://forum.sentry.io/c/on-premise)
 * [IRC](irc://chat.freenode.net/sentry) (chat.freenode.net, #sentry)
