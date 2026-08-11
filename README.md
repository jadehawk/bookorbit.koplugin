# BookOrbit KOReader Plugin

This repository is the automated distribution mirror for the BookOrbit KOReader plugin.

The source of truth is:

`bookorbit/bookorbit/koreader-plugin/bookorbit.koplugin`

Plugin code is developed and reviewed in the main BookOrbit repository. Do not submit plugin implementation changes here; submit them to `bookorbit/bookorbit` instead.

## Installation

Download `bookorbit.koplugin.zip` from the latest GitHub Release, extract it, and copy `bookorbit.koplugin/` into your KOReader `plugins/` directory. Restart KOReader, then configure the BookOrbit server and login from **Tools > BookOrbit**.

This repository is also intended for discovery and installation through KOReader Storefront.

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
