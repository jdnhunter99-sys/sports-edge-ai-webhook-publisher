# Sports Edge AI PropLine Webhook Publisher

This repository owns the PropLine webhook cache and daily grading pipeline.

- `propline_webhook` repository dispatches update per-sport JSON cache files.
- The daily workflow grades unresolved rows through the PropLine results API.
- Published rows live on the `Propline-Webhook-Cache` branch under `data/propline-webhook-cache/v1/`.
- `workflow_dispatch` on the publisher runs its mapping/first-price self-test and initializes empty cache files.

## Connect the production pipeline

1. Create the GitHub repository `jdnhunter99-sys/sports-edge-ai-webhook-publisher` and push both local branches: `main` and `Propline-Webhook-Cache`.
2. Add the repository secret `PROPLINE_API_KEY` for daily grading.
3. In the Cloudflare Worker, change the GitHub dispatch URL to `https://api.github.com/repos/jdnhunter99-sys/sports-edge-ai-webhook-publisher/dispatches`. The `GITHUB_TOKEN` secret must be authorized for this repository and have contents write access.
4. Keep the published cache branch publicly readable if the app fetches it through `raw.githubusercontent.com`.
5. The app source has been pointed at the new repository's published branch. The URL will return 404 until the new repository and cache branch are pushed.

The current Cloudflare Worker is managed in Cloudflare and is not changed by this local repository split.
