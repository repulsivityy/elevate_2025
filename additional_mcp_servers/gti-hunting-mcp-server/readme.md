# GTI Hunting MCP Server

A Model Context Protocol (MCP) server that provides integration with Google Threat Intelligence API endpoints for creating hunting rulesets and IOC collections.

## Features

- **Zero Dependencies**: Built using only Node.js built-in modules
- **Cross-Platform**: Works on macOS, Linux, and Windows
- **GTI Integration**: 
  - Create hunting rulesets in Livehunt with YARA rules
  - Create IOC collections with domains, URLs, IP addresses, and file hashes
  - Added Private Scanning for URLs

## Prerequisites

- Node.js 18.0.0 or higher
- GTI API key with appropriate permissions

## Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/repulsivityy/elevate_2025
   cd additional_mcp_servers/gti-hunting-mcp-server
   ```

2. **Get your GTI API key**:
   - Go to your profile and copy your API key
   
3. **Set environment variable**:
   ```bash
   # Linux/macOS
   export GTI_APIKEY="your-api-key-here"
   
   # Windows
   set GTI_APIKEY=your-api-key-here
   ```

## Usage

### Running the Server

```bash
# Navigate to the project directory
cd additional_mcp_servers/gti-hunting-mcp-server

# Start the server
GTI_APIKEY="your-api-key" node server.js
```

### Available Tools

#### 1. create_hunting_ruleset
Creates a new hunting ruleset in Livehunt.

**Parameters:**
- `name` (required): Name of the hunting ruleset
- `rules` (required): YARA rules content
- `enabled` (optional): Whether the ruleset should be enabled (default: false)

#### 2. create_collection
Creates a new IOC collection in Google Threat Intelligence.

**Parameters:**
- `name` (required): Name of the collection
- `description` (optional): Description of the collection
- `domains` (optional): Array of domain names
- `urls` (optional): Array of URLs
- `ip_addresses` (optional): Array of IP addresses
- `file_hashes` (optional): Array of file hashes (MD5/SHA1/SHA256)

## Integration with MCP Clients

### Claude Desktop
Add to your Claude Desktop configuration:
```json
{
  "mcpServers": {
    "gti-hunting": {
      "command": "node",
      "args": ["/path/to/gti-hunting-mcp-server/server.js"],
      "env": {
        "GTI_APIKEY": "your-api-key-here"
      }
    }
  }
}
```

### Other MCP Clients
This server works with any MCP-compatible client. Refer to your client's documentation for configuration details.

## Common Errors & Troubleshooting

### API Key Issues
- **"GTI_APIKEY environment variable not set"**
  - Make sure you've set the environment variable correctly
  - Verify the variable name is exactly `GTI_APIKEY`

- **"Wrong API key" error (401)**
  - Verify your API key is correct

### Permission Errors
- **"Access denied" error (403)**
  - Livehunt requires VirusTotal Enterprise / Google Threat Intelligence account
  - Verify your API key has the necessary permissions

### IOC Collection Errors
- **"No IOCs provided" error**
  - Collections must contain at least one IOC (domain, URL, IP address, or file hash)
  - Make sure you're providing IOCs in the correct parameter arrays

### Connection Issues
- **Request timeout or network errors**
  - Check your internet connection
  - Verify Google Threat Intelligence service status
  - Ensure no firewall is blocking HTTPS connections

### Server Issues
- **Server not responding**
  - Ensure Node.js 18+ is installed
  - Check the server process is running
  - Verify your MCP client configuration

## Important Notes

- **Auto-tagging**: All created items are automatically tagged with "-Elevate2025" suffix and "automatically created via cline / mcp" in descriptions
- **VT Module**: YARA rules automatically include `import "vt"` for advanced GTI features
- **Safety**: Hunting rulesets are created as disabled by default
- **No Persistence**: The server is stateless and doesn't store any data locally


## API Reference

- [Google Threat Intelligence Livehunt API](https://gtidocs.virustotal.com/reference/create-hunting-ruleset)
- [Google Threat Intelligence Collections API](https://gtidocs.virustotal.com/reference/create-ioc-collection)
- [MCP Protocol Specification](https://modelcontextprotocol.io/docs/specification)

## License

MIT License - feel free to modify and distribute.