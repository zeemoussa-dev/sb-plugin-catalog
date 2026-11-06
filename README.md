# sb-plugin-catalog

The official plugin catalog for Second Brain OS (framework `ADR-139`, `REQ-SB-115`).

Every install reads `catalog.json` from this repository when someone presses
**Check for updates** in the Marketplace. A plugin listed here reaches every
install from then on, with no change to the framework.

## Adding a plugin

Add one line to `plugins` in `catalog.json` and commit:

```json
{"repo": "https://github.com/zeemoussa-dev/sb-plugins-example"}
```

- `repo` is the plugin's Git repository; `owner/name` works for GitHub too.
- `ref` is optional: a branch or tag to read instead of the default branch.

Nothing else goes here. The plugin's own `plugin.json` says its name, version,
framework API, category and what it requires, and the Marketplace reads it from
the repository. A plugin built for another framework API is counted but not offered.

## The format

```json
{
  "name": "Second Brain",
  "plugins": [{"repo": "https://github.com/owner/name", "ref": null}]
}
```

`name` is how an install labels the plugins this catalog lists. An entry that is
not an object or has no `repo` is skipped, never fatal.

## Other catalogs

An install can read more than one catalog: Admin Center > Marketplace >
Catalogs > Manage. A team keeps its own repository in this same shape, and adds
it there. A private catalog is read with the Marketplace's GitHub token.

## The framework's snapshot

The framework ships a copy of this file
(`src/backend/app/business/core/marketplace/catalog.json`), used only by an
install that has never read this repository, for example one with no internet.
Copy this file there now and then; it is not where plugins are added.
