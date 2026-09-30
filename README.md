# Coherent Paradox

Static website deployed by GitHub Pages from the root of `master`, matching the deployment strategy used for gustavosilva.me. Every push to `master` publishes automatically; no custom build workflow or hosting subscription is required.

- `/actor-terms/`: approved Actor contract, with navigation and PDF download.
- `/actor-terms/contract.pdf`: downloadable contract.
- Homepage and other paths: redirect to https://gustavosilva.me/.

## Update the terms

1. Edit `actor-terms.md`. Preserve its YAML front matter.
2. Replace `actor-terms/contract.pdf` with the matching PDF.
3. Commit and push to `master` (or review changes in a pull request first).

Git history preserves previous versions. To undo an update, revert its commit and push.

The website publishes the contract text approved in the merged contract review. Publishing it does not submit it to Apify or change any Actor listing.

See [DEPLOYMENT.md](DEPLOYMENT.md) for domain configuration.
