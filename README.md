# BookOrbit KOReader Plugin

This repository is the automated distribution mirror for the BookOrbit KOReader plugin. Its purpose is to make the plugin available as a standalone distribution and discoverable by KOReader plugin catalogs such as [Storefront](https://github.com/ultimatejimmy/storefront.koplugin).

The source of truth is the [BookOrbit repository](https://github.com/bookorbit/bookorbit). Plugin code is developed and reviewed there; do not submit plugin implementation changes to this distribution mirror.

## Installation

### Recommended: BookOrbit UI

Use the BookOrbit web UI to download a pre-configured plugin. This package includes your BookOrbit server configuration, making it the preferred and simplest installation method.

### Alternative: Manual installation

Download `bookorbit.koplugin.zip` from the latest GitHub Release, extract it, and copy `bookorbit.koplugin/` into your KOReader `plugins/` directory. Restart KOReader, then configure the BookOrbit server and login from **Tools > BookOrbit**.

### Alternative: Storefront

If you have [Storefront](https://github.com/ultimatejimmy/storefront.koplugin) installed in KOReader, look for the BookOrbit plugin in its plugin catalog and install it from there.

## Automated synchronization

A GitHub Actions workflow checks BookOrbit upstream every six hours and can also be run manually. It fingerprints only `koreader-plugin/bookorbit.koplugin/`, so unrelated BookOrbit server or web changes do not create plugin releases.

When the plugin changes, the workflow:

1. Reads `PLUGIN_VERSION` from upstream `main.lua`.
2. Refuses to publish if that version already has a release tag, requiring the upstream plugin version to be bumped for every distributable change.
3. Runs the complete upstream KOReader Lua test suite with Lua 5.1.
4. Copies the generic plugin source into this repository.
5. Verifies that no embedded BookOrbit configuration or credentials are present.
6. Builds `bookorbit.koplugin.zip` with `bookorbit.koplugin/` as the archive root.
7. Commits the synchronized source and creates the matching `vX.Y.Z` GitHub Release with the ZIP attached.

## License

BookOrbit is distributed under the GNU Affero General Public License v3.0. See [LICENSE](LICENSE).
