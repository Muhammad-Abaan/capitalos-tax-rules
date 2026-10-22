# CapitalOS tax rules

The official tax rule packs that every copy of CapitalOS downloads to keep its tax calculations current.

- `packs/*.json`: one pack per country and tax year. Each pack holds the slabs, rates, limits and due dates, every value with the section of the law and the source it comes from.
- `manifest.json`: each pack's id, version and SHA-256 hash.
- `manifest.sig`: an Ed25519 signature of `manifest.json`. The app checks it with the public key built into it, then checks each pack's hash and contents. Anything that doesn't match is refused.

## Publishing a change

Don't edit these files by hand: a changed file without a new signature is refused by every app.

1. In the CapitalOS project, edit the pack in `src/data/tax/` and raise its `"version"`. Add a plain-language line to `"changelog"` and update the sources.
2. Run `node scripts/tax-packs.mjs publish <private key> <this folder>`.
3. Commit and push this folder. Apps pick it up within a day.

The private signing key never goes in any repository.
