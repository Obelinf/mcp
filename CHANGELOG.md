# Changelog

Notable changes to the Obelinf MCP server: new tools, endpoint behavior, and connection docs. This file tracks the MCP surface itself; the changelog of your organization's data lives inside Obelinf (tool: `list_changelog`).

## [1.0.1] - 2026-08-30

### Changed

- Endpoint moved from `https://api.obelinf.com/{orgSlug}/mcp` to `https://api.obelinf.com/mcp?org={orgSlug}`. The organization is now passed as a query parameter, giving the MCP server a stable URL that works with directory gateways that require a fixed upstream URL (e.g. Smithery).

## [1.0.0] - 2026-08-30

### Added

- Initial publication to the official MCP Registry (`io.github.Obelinf/mcp`), remote endpoint `https://api.obelinf.com/{orgSlug}/mcp` (Streamable HTTP).
- 52 tools:
  - `search`: cross-resource full-text search
  - Sites, racks, devices, subnets, IP addresses, VLANs, VRFs, cables, MAC addresses, and contacts: full `list_*` / `get_*` / `create_*` / `update_*` / `delete_*` coverage for each
  - `list_changelog`: audit trail of every change, with actor and field-level diffs
- Authentication via scoped API keys (`Read Only` / `Full Access`) sent as `Authorization: Bearer`.
- MCP access available on all plans, including the free Personal plan.
