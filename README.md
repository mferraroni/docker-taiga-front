[![](https://badge.imagelayers.io/beevelop/taiga-front:latest.svg)](https://imagelayers.io/?images=beevelop/taiga-front:latest 'Get your own badge on imagelayers.io')

# beevelop/taiga-front (adapted from htdvisser/taiga-front-dist)
> [Taiga](https://taiga.io/) is a project management platform for startups and agile developers & designers who want a simple, beautiful tool that makes work truly enjoyable.

This Docker image can be used for running the Taiga frontend. It works together with the [beevelop/taiga-back](https://registry.hub.docker.com/u/beevelop/taiga-back/) image.

## Running

A [beevelop/taiga-back](https://registry.hub.docker.com/u/beevelop/taiga-back/) needs to be linked as `taigaback`. Also connect the volumes of the taiga-back container if you want to serve the static files for the admin panel.

```bash
docker run --name taiga_front_container --link taiga_back_container:taigaback --volumes-from taiga_back_container beevelop/taiga-front
```

## Environment
* `PUBLIC_REGISTER_ENABLED`: defaults to the respective **Taiga-Back** configuration or `true`
* `FEEDBACK_ENABLED`: defaults to the respective **Taiga-Back** configuration or `true`
* `GITHUB_API_CLIENT_ID`: provide a GitHub API ID to enable GitHub OAuth
* `DEFAULT_LANGUAGE`: defaults to `en`
* `DEFAULT_THEME`: defaults to `taiga` (also available (as of Taiga's source code), but untested: `material-design`, `high-contrast`)
  * Feedback on these settings is appreciated

## Sign-Up / Register
Users will have to accepts those terms in order to register. Therefore these settings are only relevant if `PUBLIC_REGISTER_ENABLED` is `true`
* `PRIVACY_POLICY_URL`: provide an URL to your own privacy policy (default `null`)
* `TERMS_OF_SERVICE_URL`: provide an URL to your own TOS (default `null`)

## API and SSL
* ``API`` defaults to ``"/api/v1"``
* ``SCHEME`` defaults to ``http``. If ``https`` is used either
  * ``SSL_CRT`` and ``SSL_KEY`` needs to be set **or**
  * ``/etc/nginx/ssl/`` volume attached with ``ssl.crt`` and ``ssl.key`` files
* ``SSL_CRT`` SSL certificate value. Valid only when ``SCHEME`` set to https.
* ``SSL_KEY`` SSL certificate key. Valid only when ``SCHEME`` set to https.

## Debugging
* ``DEBUG_ENTRYPOINT``: set to True to enable Debugging (`set -x`)
* ``DEBUG`` defaults to ``false``

## SSL Support
HTTPS can be enabled by setting ``SCHEME`` to ``https`` and filling ``SSL_CRT``
and ``SSL_KEY`` env variables (see Environment section below). *http* (port 80)
requests will be redirected to *https* (port 443).