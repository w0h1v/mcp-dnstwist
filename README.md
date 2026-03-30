# DNStwist MCP Server
[![smithery badge](https://smithery.ai/badge/@burtthecoder/mcp-dnstwist)](https://smithery.ai/server/@burtthecoder/mcp-dnstwist)

A Model Context Protocol (MCP) server for [dnstwist](https://github.com/elceef/dnstwist), a powerful DNS fuzzing tool that helps detect typosquatting, phishing, and corporate espionage. This server provides tools for analyzing domain permutations and identifying potentially malicious domains. It is designed to integrate seamlessly with MCP-compatible applications like [Claude Desktop](https://claude.ai).

<a href="https://glama.ai/mcp/servers/it7izu3ufb"><img width="380" height="200" src="https://glama.ai/mcp/servers/it7izu3ufb/badge" alt="mcp-dnstwist MCP server" /></a>


## ⚠️ Warning

This tool is designed for legitimate security research purposes. Please:
- Only analyze domains you own or have permission to test
- Respect rate limits and DNS server policies
- Use responsibly and ethically
- Be aware that some DNS servers may rate-limit or block automated queries
- Consider the impact on DNS infrastructure when running large scans

## Requirements

- Node.js (v18 or later)
- Docker
- macOS, Linux, or Windows with Docker Desktop installed

## Quick Start

### Installing via Smithery

To install DNStwist for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@burtthecoder/mcp-dnstwist):

```bash
npx -y @smithery/cli install @burtthecoder/mcp-dnstwist --client claude
```

### Installing Manually
1. Install Docker:
   - macOS: Install [Docker Desktop](https://www.docker.com/products/docker-desktop)
   - Linux: Follow the [Docker Engine installation guide](https://docs.docker.com/engine/install/)

2. Install the server globally via npm:
```bash
npm install -g mcp-dnstwist
```

3. Add to your Claude Desktop configuration file:
```json
{
  "mcpServers": {
    "dnstwist": {
      "command": "mcp-dnstwist"
    }
  }
}
```

Configuration file location:
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

4. Restart Claude Desktop

## Hosted deployment

A hosted deployment is available on [Fronteir AI](https://fronteir.ai/mcp/burtthecoder-mcp-dnstwist).

## Alternative Setup (From Source)

If you prefer to run from source or need to modify the code:

1. Clone and build:
```bash
git clone <repository_url>
cd mcp-dnstwist
npm install
npm run build
```

2. Add to your Claude Desktop configuration:
```json
{
  "mcpServers": {
    "dnstwist": {
      "command": "node",
      "args": ["/absolute/path/to/mcp-dnstwist/build/index.js"]
    }
  }
}
```

## Features

- **Domain Fuzzing**: Generate domain permutations using various algorithms
- **Registration Check**: Verify if permutated domains are registered
- **DNS Analysis**: Check A, AAAA, MX, and NS records
- **Web Presence**: Capture HTTP banner information
- **WHOIS Data**: Retrieve registration dates and registrar information
- **Phishing Detection**: Generate fuzzy hashes of web pages
- **Configurable**: Custom DNS servers and parallel processing
- **Multiple Formats**: Support for json, csv, and list output formats

## Tools

### Domain Fuzzing Tool
- Name: `fuzz_domain`
- Description: Generate and analyze domain permutations to detect potential typosquatting, phishing, and brand impersonation
- Parameters:
  * `domain` (required): Domain name to analyze (e.g., example.com)
  * `nameservers` (optional, default: "1.1.1.1"): Comma-separated list of DNS servers
  * `threads` (optional, default: 50): Number of threads for parallel processing
  * `format` (optional, default: "json"): Output format (json, csv, list)
  * `registered_only` (optional, default: true): Show only registered domains
  * `mxcheck` (optional, default: true): Check for MX records
  * `ssdeep` (optional, default: false): Generate fuzzy hashes of web pages
  * `banners` (optional, default: true): Capture HTTP banner information

Example:
```json
{
  "domain": "example.com",
  "nameservers": "1.1.1.1,8.8.8.8",
  "threads": 50,
  "format": "json",
  "registered_only": true,
  "mxcheck": true,
  "banners": true
}
```

## Troubleshooting

### Docker Issues

1. Verify Docker is installed and running:
```bash
docker --version
docker ps
```

2. Check Docker permissions:
   - Ensure your user has permissions to run Docker commands
   - On Linux, add your user to the docker group: `sudo usermod -aG docker $USER`

### Common Issues

1. DNS resolution problems:
   - Verify DNS servers are accessible
   - Try alternative DNS servers (e.g., 8.8.8.8)
   - Check for rate limiting or blocking

2. Performance issues:
   - Adjust thread count based on system capabilities
   - Consider network bandwidth and latency
   - Monitor DNS server response times

3. After fixing any issues:
   - Save the configuration file
   - Restart Claude Desktop

## Error Messages

- "Docker is not installed or not running": Install Docker and start the Docker daemon
- "Failed to parse dnstwist output": Check if the domain is valid and the format is correct
- "Error executing dnstwist": Check Docker logs and ensure proper permissions
- "DNS server not responding": Verify DNS server accessibility and try alternative servers

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
