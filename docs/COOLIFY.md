# Coolify deployment

Create an application connected to your repository and select the branch
you want to deploy. The configuration below uses `globe.example.com` as an
example domain; replace it with your own hostname.

Use the repository's `/Dockerfile`, build context `/`, and internal port
`4173`. Do not publish a host port. The Vite server serves both the globe and
its provider middleware; a static-only deployment would omit the data APIs.
The Dockerfile supplies an HTTP health check with a two-minute startup grace
period. Disable Coolify's generated health check to retain that check.

Set these runtime-only variables in Coolify:

```dotenv
HOST=0.0.0.0
PORT=4173
GEV_ALLOWED_HOSTS=globe.example.com
GEV_KEY_SETUP_TRUSTED_PEERS=127.0.0.1
OPENSKY_AUTH_MODE=anon
```

No provider key or database is required. The explicit trusted peer prevents
the Docker launcher from trusting its network gateway for Provider Settings.
Public requests through the reverse proxy cannot administer keys or the local
MCP endpoint. If provider keys are added later, manage them as runtime secrets
in Coolify; never place them in Git or Docker build arguments.

Connect the repository through a GitHub App. Enable automatic deployment
on push to the selected branch, use commit `HEAD`, disable pull request previews,
and enable HTTPS. Keep build-argument injection disabled.

DNS: create an `A` record for your hostname pointing to the deployment server.
Coolify terminates HTTPS and routes to port `4173` on its private Docker network.
The app's cache is disposable and is rebuilt when the container is replaced.

After deployment, verify HTTPS, JavaScript/CSS delivery, a public data API,
and refusal of `/api/setup/status` through the public domain. Check Coolify's
deployment record to confirm that the Git push triggered a webhook deployment.
