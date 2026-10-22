# Coolify deployment

The MERZA instance runs at `https://eye.merza.fr`, from the `main` branch of
`nicoduchR/gods-eye-view`. The original project remains available through the
local `origin` Git remote; the deployment fork uses the `merza` remote.

Use the repository's `/Dockerfile`, build context `/`, and internal port
`4173`. Do not publish a host port. The Vite server serves both the globe and
its provider middleware; a static-only deployment would omit the data APIs.
The Dockerfile supplies an HTTP health check with a two-minute startup grace
period. Disable Coolify's generated health check to retain that check.

Set these runtime-only variables in Coolify:

```dotenv
HOST=0.0.0.0
PORT=4173
GEV_ALLOWED_HOSTS=eye.merza.fr
GEV_KEY_SETUP_TRUSTED_PEERS=127.0.0.1
OPENSKY_AUTH_MODE=anon
```

No provider key or database is required. The explicit trusted peer prevents
the Docker launcher from trusting its network gateway for Provider Settings.
Public requests through the reverse proxy cannot administer keys or the local
MCP endpoint. If provider keys are added later, manage them as runtime secrets
in Coolify; never place them in Git or Docker build arguments.

Connect the fork through the existing GitHub App. Enable automatic deployment
on push to `main`, use commit `HEAD`, disable pull request previews, and enable
HTTPS. Keep build-argument injection disabled. Updates to the original project
must be reviewed and pushed to the fork before they reach this instance.

DNS: create an `A` record for `eye.merza.fr` pointing to `195.35.0.213`.
Coolify terminates HTTPS and routes to port `4173` on its private Docker network.
The app's cache is disposable and is rebuilt when the container is replaced.

After deployment, verify HTTPS, JavaScript/CSS delivery, a public data API,
and refusal of `/api/setup/status` through the public domain. Check Coolify's
deployment record to confirm that the Git push triggered a webhook deployment.
