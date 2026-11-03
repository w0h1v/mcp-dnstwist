# Connect a client

mcp-dnstwist speaks MCP over stdio. It needs Node.js 20.3 or newer, plus one way to run dnstwist:

| Runner | Needs | Notes |
|---|---|---|
| **Local** | `dnstwist` on your `PATH` (`pipx install "dnstwist[full]"`) | Fastest, no Docker. Used automatically when found. |
| **Docker** | Docker running | Uses the `elceef/dnstwist` image (pulled on first start). The image is amd64-only, so it runs under emulation on Apple Silicon. |

`DNSTWIST_RUNNER` picks one explicitly (`local`, `docker`, or the default `auto`). No API key is needed.

## Claude Code

```sh
claude mcp add --transport stdio dnstwist -- npx -y @burtthecoder/mcp-dnstwist
claude mcp get dnstwist      # should show: Connected
```

## Codex CLI

```sh
codex mcp add dnstwist -- npx -y @burtthecoder/mcp-dnstwist
```

## Gemini CLI

```sh
gemini mcp add dnstwist npx -y @burtthecoder/mcp-dnstwist
```

## Claude Desktop

Edit the config file, then restart the app.

| OS | Path |
|---|---|
| macOS | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Windows | `%APPDATA%\Claude\claude_desktop_config.json` |

```json
{
  "mcpServers": {
    "dnstwist": {
      "command": "npx",
      "args": ["-y", "@burtthecoder/mcp-dnstwist"]
    }
  }
}
```

Desktop apps may not see your shell's `PATH`, so they might not find `docker` or `dnstwist`. If the server reports that neither is available, add an `env` block with your `PATH`, or set `DNSTWIST_RUNNER` and use absolute paths.

## VS Code (GitHub Copilot)

Create `.vscode/mcp.json` in your workspace, or add the server with **MCP: Add Server**, then reload VS Code.

```json
{
  "servers": {
    "dnstwist": {
      "command": "npx",
      "args": ["-y", "@burtthecoder/mcp-dnstwist"]
    }
  }
}
```

## Docker (no Node or dnstwist on the host)

The mcp-dnstwist image bundles Node and dnstwist, so it doesn't need access to your Docker daemon.

```sh
docker build -t mcp-dnstwist https://github.com/w0h1v/mcp-dnstwist.git
```

```json
{
  "mcpServers": {
    "dnstwist": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "mcp-dnstwist"]
    }
  }
}
```

## From source

```sh
git clone https://github.com/w0h1v/mcp-dnstwist && cd mcp-dnstwist
npm ci && npm run build
```

Use the command `node` with the argument `/absolute/path/to/mcp-dnstwist/build/index.js`.

## Settings

| Variable | Default | Description |
|---|---|---|
| `DNSTWIST_RUNNER` | `auto` | `local`, `docker`, or `auto` (local if `dnstwist` is on `PATH`, otherwise Docker) |
| `DNSTWIST_TIMEOUT_SECONDS` | `600` | Longest a scan may run before it's stopped and cleaned up |

Set them in the client's `env` block, for example `"env": { "DNSTWIST_RUNNER": "docker" }`.
