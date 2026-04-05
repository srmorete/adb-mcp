# ARCHIVED -- Use [mobile-device-mcp](https://github.com/srmorete/mobile-device-mcp)
Quite surprised that this repo reached 50 stars (!) the ecosystem is quite generous sometimes, thank you for starring it!

I've been working on something that is faster, more scalable and also works with iOS, take a look at [mobile-device-mcp](https://github.com/srmorete/mobile-device-mcp).

And leave some ⭐ too :) 


## ADB MCP Server
[![smithery badge](https://smithery.ai/badge/@srmorete/adb-mcp)](https://smithery.ai/server/@srmorete/adb-mcp)

An MCP (Model Context Protocol) server for interacting with Android devices through ADB. This TypeScript-based tool provides a bridge between AI models and Android device functionality.

## Features

- 📱 Device Management - List and interact with connected Android devices
- 📦 App Installation - Deploy APK files to connected devices
- 📋 Logging - Access device logs through logcat
- 🔄 File Transfer - Push and pull files between device and host
- 📸 UI Interaction - Capture screenshots and analyze UI hierarchy
- 🔧 Shell Command Execution - Run custom commands on the device

## Prerequisites

- Node.js (v16 or higher recommended, tested with Node.js v16, v18, and v20)
- ADB (Android Debug Bridge) installed and in your PATH
- An Android device or emulator connected via USB or network with USB debugging enabled
- Permission to access the device (accepted debugging authorization on device)

## Installation

### Installing via Smithery

To install ADB Android Device Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@srmorete/adb-mcp):

```bash
npx -y @smithery/cli install @srmorete/adb-mcp --client claude
```

### Manual Installation
```bash
# Clone the repository
git clone https://github.com/srmorete/adb-mcp.git
cd adb-mcp

# Install dependencies
npm install

# Build the TypeScript code
npm run build

# Run the server
npx adb-mcp
```

## Configuration

### ADB Path Configuration

The server uses default ADB paths. For custom ADB location:

```bash
export ADB_PATH=/path/to/adb
npx adb-mcp
```

### MCP Configuration

Add the ADB MCP server configuration:
   ```json
   {
     "mcpServers": {
       "adb": {
         "command": "npx",
         "args": [
           "adb-mcp"
         ]
       }
     }
   }
   ```

## Usage

### Starting the Server

**IMPORTANT: The server must be running before using any ADB tools.**

Start the server using:

```bash
npx adb-mcp
```

You should see:
```
[INFO] ADB MCP Server connected and ready
```

Keep this terminal window open while using the ADB tools.

### Available Tools

All tools are available with the following naming convention:

#### 📱 Device Management

- `adb_devices` - List connected devices
- `adb_shell` - Execute shell commands on a device

#### 📦 App Management

- `adb_install` - Install an APK file using a local file path
- `adb_package_manager` - Execute Package Manager (pm) commands - list packages, grant/revoke permissions, manage apps
- `adb_activity_manager` - Execute Activity Manager (am) commands - start activities, broadcast intents, control app behavior

#### 📋 Logging

- `adb_logcat` - View device logs with optional filtering

#### 🔄 File Transfer

- `adb_pull` - Pull files from a device
- `adb_push` - Push files to a device

#### 🔍 UI Interaction

- `dump_image` - Take a screenshot of the current screen
- `inspect_ui` - Get UI hierarchy in XML format (most useful for AI interaction)

## Troubleshooting

If tools aren't working:

- **Server Issues:**
  - Ensure the server is running (`npx adb-mcp`)
  - Check server output for error messages
  - Try detailed logs: `LOG_LEVEL=3 npx adb-mcp`
  - Kill hanging processes:
    - `ps aux | grep "adb-mcp" | grep -v grep`
    - then `kill -9 [PID]`

- **Device Connection:**
  - Verify connection with `adb_devices`
  - If "unauthorized", accept debugging authorization on device
  - Check USB/network connections
  - Try restarting ADB: `adb kill-server && adb start-server`

- **ADB Issues:**
  - Verify ADB installation: `adb version`

- **Device Setup:**
  - Use an emulator (it was built using one), for real devices maybe try this:
    - Ensure USB debugging is enabled
    - For newer Android versions, enable "USB debugging (Security settings)"
    - Try different USB port or cable
    - or let me know in an issue

## Compatibility

- Android 8.0 and higher
- MCP clients including Claude in Cursor IDE
- Was built on macOS but **should** run on any POSIX compatible (Linux etc).
- Did not try on Windows but **maybe** it works.

## Contributing

- Contributions are welcome! Submit a Pull Request.
- For major changes, open an issue to discuss first.
- You can, of course, also fork it
- **Note:** this project was `vibe-coded` so if you spot some weird stuff... well now you know 🙂

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built with [Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction)
