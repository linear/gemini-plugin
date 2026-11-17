# Changelog

All notable changes to this plugin are documented here. This project follows [Semantic Versioning](https://semver.org/).

## [1.0.1] - 2026-11-17

### Changed

- `linear-workspace` skill now includes the Linear MCP server's cross-tool guidance (references, paging, team-scoped values, comments, images, `save_*` updates, labels, and Markdown), because Gemini does not pass the server's `initialize` instructions to the model.

## [1.0.0] - 2026-11-17

### Added

- Gemini plugin manifest at `.gemini-plugin/plugin.json`.
- `.mcp.json` with the hosted Linear MCP server at `https://mcp.linear.app/mcp`.
- `linear-workspace` skill with general rules for working in Linear through the MCP server.
