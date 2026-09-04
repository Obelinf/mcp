# Obelinf MCP Server

Hosted [Model Context Protocol](https://modelcontextprotocol.io) server for [Obelinf](https://obelinf.com), the network and infrastructure documentation platform. Connect AI agents like Claude, Cursor, or Codex to your infrastructure records and let them query, answer, and update sites, racks, devices, IP address space, and cabling through one endpoint.

> This repository does not contain the server's source code. It holds the MCP listing metadata, connection docs, the changelog for the MCP surface, and the public issue tracker.

- Website: <https://obelinf.com>
- API documentation: <https://obelinf.com/docs/api/>
- MCP feature overview: <https://obelinf.com/features/ai-infrastructure-documentation/>

## Quick start

1. **Sign in** at [obelinf.com](https://obelinf.com) and open your organization. MCP is available on **all plans**, including the free Personal plan.
2. **Create an API key**: Dashboard → **API Keys** → create a key and choose a scope: `Read Only` or `Full Access`. Copy it when shown; it is only displayed once.
3. **Add the server** to your MCP client. Your endpoint is `https://api.obelinf.com/mcp`. The organization is selected from your authenticated Obelinf account.

### ChatGPT

ChatGPT uses OAuth. Add the MCP endpoint and complete the Obelinf approval flow when prompted. Google and GitHub remain the available Obelinf sign-in methods; ChatGPT receives a short-lived, organization-scoped MCP token after approval.

### Cursor (plugin)

Install the `Obelinf/mcp` repository as a Cursor plugin from the [Cursor directory](https://cursor.directory). Set `OBELINF_API_KEY` once under **Plugins → Configure** and the server connects automatically. No manual JSON editing needed.

To add it manually instead, use the config below.

### Claude Code

```bash
claude mcp add --transport http obelinf "https://api.obelinf.com/mcp" \
  --header "Authorization: Bearer YOUR_API_KEY"
```

### Claude Desktop, Cursor, and other JSON-configured clients

```json
{
  "mcpServers": {
    "obelinf": {
      "url": "https://api.obelinf.com/mcp",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

### VS Code (.vscode/mcp.json)

```json
{
  "servers": {
    "obelinf": {
      "type": "http",
      "url": "https://api.obelinf.com/mcp",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

Other MCP clients: point them at the URL above over Streamable HTTP and send the API key as an `Authorization: Bearer` header.

## Endpoint details

| Property | Value |
| --- | --- |
| Endpoint | `https://api.obelinf.com/mcp` |
| Transport | MCP Streamable HTTP |
| Authentication | OAuth for ChatGPT; scoped API keys for other clients |
| Rate limit | 100 requests per minute |
| Availability | All plans |
| Tools | 52 |

## Tools

| Group | Tools | Description |
| --- | --- | --- |
| Search | `search` | Cross-resource full-text search across your inventory |
| Sites | `list_sites`, `get_site`, `create_site`, `update_site`, `delete_site` | Physical locations and data center sites |
| Racks | `list_racks`, `get_rack`, `create_rack`, `update_rack`, `delete_rack` | Rack inventory, units, and positions |
| Devices | `list_devices`, `get_device`, `create_device`, `update_device`, `delete_device` | Servers, switches, appliances, and VMs |
| Subnets | `list_subnets`, `get_subnet`, `create_subnet`, `update_subnet`, `delete_subnet` | IPAM subnets and prefixes |
| IP addresses | `list_ip_addresses`, `get_ip_address`, `create_ip_address`, `update_ip_address`, `delete_ip_address` | Assigned and free addresses |
| VLANs | `list_vlans`, `get_vlan`, `create_vlan`, `update_vlan`, `delete_vlan` | VLAN groups and IDs |
| VRFs | `list_vrfs`, `get_vrf`, `create_vrf`, `update_vrf`, `delete_vrf` | Virtual routing and forwarding instances |
| Cables | `list_cables`, `get_cable`, `create_cable`, `update_cable`, `delete_cable` | Cabling between ports and endpoints |
| MAC addresses | `list_mac_addresses`, `get_mac_address`, `create_mac_address`, `update_mac_address`, `delete_mac_address` | MAC inventory and assignments |
| Contacts | `list_contacts`, `get_contact`, `create_contact`, `update_contact`, `delete_contact` | People and vendors tied to infrastructure |
| Changelog | `list_changelog` | Audit trail of every change, with actor and field-level diffs |

### Permissions

- **Read Only** keys can use all read and search tools. Write tools return an error.
- **Full Access** keys can read and write. Every write is recorded in the organization changelog with attribution and field-level diffs, so agent edits are as reviewable as manual ones.

Start agents on a Read Only key, review their diffs, then promote to Full Access deliberately.

## Support

- Bug reports and feature requests for the MCP surface: [open an issue](https://github.com/Obelinf/mcp/issues)
- Plans, pricing, and enterprise agreements: [Contact sales](https://obelinf.com/contact/sales/)
