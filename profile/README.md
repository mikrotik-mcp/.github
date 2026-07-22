<div align="center">
  <img src="https://raw.githubusercontent.com/mikrotik-mcp/mikrotik-mcp/refs/heads/master/assets/logo.svg" alt="mikrotik-mcp" width="440" />
  <p><strong>Drive one or more MikroTik routers from your AI — 800+ tools over SSH.</strong><br/>
  Firewall · routing · DHCP/DNS · wireless · QoS · full VPN suite — with transactional Safe Mode.</p>

  <p>
    <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-7C3AED.svg"></a>
    <img alt="Runtime: Bun" src="https://img.shields.io/badge/runtime-Bun%20%E2%89%A5%201.3-06B6D4.svg">
    <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-strict-6366F1.svg">
    <img alt="MCP" src="https://img.shields.io/badge/MCP-794%20tools-1F2937.svg">
    <a href="https://mikrotik-mcp.usestrict.dev"><img alt="Docs" src="https://img.shields.io/badge/docs-reference-7C3AED.svg"></a>
  </p>
</div>

---

**mikrotik-mcp** exposes **MikroTik RouterOS** as **794 [Model Context Protocol](https://modelcontextprotocol.io) tools across 124 modules**, so any MCP client (Claude Desktop, Claude Code, your own agent) can read and configure your router in plain language. It talks to the device over **SSH** — nothing to install on RouterOS — runs on **[Bun](https://bun.sh)**, and validates every call against a Zod schema.

> _"Show me the firewall input chain, then block SSH from the WAN under safe mode."_
> _"Build an IKEv2 site-to-site tunnel to 203.0.113.5 for 192.168.20.0/24."_
> _"Why can't VLAN 50 reach the internet?"_

## Why it's different

- 🧰 **Breadth** — 800+ tools covering the whole device: L2 (bridge, VLAN, wireless, PoE), L3 (addressing, routing, DHCP, DNS), security (firewall, NAT, address-lists, certificates), QoS, and system ops (users, logs, backups, scheduler).
- 🔐 **Complete VPN suite** — WireGuard, IPsec (IKEv1/IKEv2), L2TP, PPTP, SSTP, OpenVPN, plus GRE/IPIP/EoIP/VXLAN tunnels — with a prompt that picks the right one for you.
- 🛟 **Safe Mode** — a real transactional window backed by a persistent SSH session. Auto-reverts on disconnect, so you can't lock yourself out.
- 🚦 **Risk-annotated tools** — every tool carries a read/write/destructive hint, so clients auto-approve reads and prompt on writes.
- 🧱 **Injection-safe by construction** — a command builder quotes and escapes every value; a hostname like `LAN; /system reset` can never split into a second command.
- 🖧 **Multiple devices & jump hosts** — target named routers per call, configure both ends of a tunnel from one conversation, and reach portless routers through an SSH bastion.

## Quickstart

```bash
# Requires Bun ≥ 1.3 — https://bun.sh
bun add -g @usex/mikrotik-mcp

# Point it at your router and verify SSH connectivity
MIKROTIK_HOST=192.168.88.1 MIKROTIK_USERNAME=admin MIKROTIK_PASSWORD=•••• \
  mikrotik-mcp auth-check

# Serve it (stdio by default — wire into your MCP client)
mikrotik-mcp serve
```

Wire it into an MCP client:

```jsonc
// claude_desktop_config.json
{
  "mcpServers": {
    "mikrotik": {
      "command": "mikrotik-mcp",
      "env": {
        "MIKROTIK_HOST": "192.168.88.1",
        "MIKROTIK_USERNAME": "admin",
        "MIKROTIK_PASSWORD": "your-password"
      }
    }
  }
}
```

Prefer SSH keys, multiple devices, or a jump host? See the **[configuration docs](https://mikrotik-mcp.usestrict.dev)**.

## Docs

- 📖 **[Full documentation](https://mikrotik-mcp.usestrict.dev)**
- 🧩 Tool reference · VPN guide · multi-device · configuration — in [`docs/`](docs/)

## Requirements

- [Bun](https://bun.sh) ≥ 1.3
- A MikroTik device reachable over SSH (or MAC-Telnet)

---

<sub>MIT licensed · built by <a href="https://github.com/ali-master">Ali Torki</a></sub>
