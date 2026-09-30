# Coherent Paradox

Static website deployed by GitHub Pages from the root of `master`, matching the deployment strategy used for gustavosilva.me. Every push to `master` publishes automatically; no custom build workflow or hosting subscription is required.

- `/apify-actor-terms/`: approved Actor contract with section navigation.
- Homepage and other paths: redirect to https://gustavosilva.me/.

## Update the terms

1. Edit `apify-actor-terms.md`. Preserve its YAML front matter.
2. Commit and push to `master` (or review changes in a pull request first).

Git history preserves previous versions. To undo an update, revert its commit and push.

The website publishes the contract text approved in the merged contract review. Publishing it does not submit it to Apify or change any Actor listing.

See [DEPLOYMENT.md](DEPLOYMENT.md) for domain configuration.

## Branding

The original logo and icon come from Coherent Paradox → Brand in Google Drive. They are stored under `apify-actor-terms/brand/`, so the domain’s redirect exception covers them. Brand colors: charcoal `#343434` and teal `#00c6ac`; text links use a darker teal for readability.
