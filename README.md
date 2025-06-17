[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/sanchisingh01-mcp-server-gmail-plugin-for-claude-desktop-badge.png)](https://mseep.ai/app/sanchisingh01-mcp-server-gmail-plugin-for-claude-desktop)

# Gmail Plugin MCP Server

[![Python Version](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

A powerful MCP server that enables Gmail integration, allowing you to manage emails directly through MCP clients. This plugin provides seamless access to Gmail's core functionality including reading, sending, and managing emails.

> **Reference**: For a sample MCP server implementation using uvx, check out [this example](https://github.com/modelcontextprotocol/uvx/tree/main/examples/sample-mcp-server).

## 🎥 Demo

https://github.com/user-attachments/assets/df9e86cf-1f6b-4265-9c68-b3ed88103d1f

## ✨ Features

- 📧 Send and receive emails
- 📥 Read unread messages
- 🗑️ Trash emails
- 📱 Open emails in browser
- 📝 Mark emails as read
- 🔒 Secure OAuth2 authentication

## 🚀 Quick Start

### Prerequisites

- Python 3.12 or higher
- Gmail API credentials
- MCP client (like Claude Desktop)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/gmail-plugin.git
cd gmail-plugin
```

2. Install dependencies (choose one method):

```bash
# Method 1: Install in editable mode
uv pip install -e .

# Method 2: Install using requirements.txt
uv pip install -r requirements.txt

# Method 3: Install using uv sync (recommended)
uv sync --dev --all-extras
```

3. Configure your Gmail API credentials:
   - Go to [Google Cloud Console](https://console.cloud.google.com)
   - Create a new project or select existing one
   - Enable Gmail API
   - Configure OAuth consent screen:
     - Select "External" user type (no publishing required)
     - Go to the Audiences tab : Add your email as a "Test user"
     - Add OAuth scope: `https://www.googleapis.com/auth/gmail/modify` 
   - Create OAuth 2.0 credentials:
     - Choose "Desktop App" as application type
     - Download the JSON credentials file  
   - Save the credentials file and note its absolute path (will be used for `--creds-file-path`)

### Configuration

#### For Development/Unpublished Servers

Add this to your MCP client configuration:

```json
"mcpServers": {
  "gmail-plugin": {
    "command": "uv",
    "args": [
      "--directory",
      "[absolute path to working directory]",
      "run",
      "server.py"
      "--creds-file-path",
      "[absolute-path-to-credentials-file]",
      "--token-path",
      "[absolute-path-to-access-tokens-file]"
    ]
  }
}
```

#### For Published Servers

```json
"mcpServers": {
  "gmail-plugin": {
    "command": "uvx",
    "args": [
      "gmail-plugin"
    ]
  }
}
```

## 🛠️ Development

### Building and Publishing

1. Sync dependencies:
```bash
uv sync
```

2. Build package:
```bash
uv build
```

3. Publish to PyPI:
```bash
uv publish
```

### Debugging

Use the [MCP Inspector](https://github.com/modelcontextprotocol/inspector) for debugging:

```bash
npx @modelcontextprotocol/inspector uv --directory C:\Users\sanch\Desktop\gmail_plugin\gmail-plugin run gmail-plugin
```

## 📚 API Reference

### Available Tools

| Tool Name | Description | Required Arguments |
|-----------|-------------|-------------------|
| `send-email` | Send an email | recipient_id, subject, message |
| `get-unread-emails` | Retrieve unread emails | None |
| `read-email` | Read email content | email_id |
| `trash-email` | Move email to trash | email_id |
| `mark-email-as-read` | Mark email as read | email_id |
| `open-email` | Open email in browser | email_id |

### Available Prompts

| Prompt Name | Description | Arguments |
|-------------|-------------|-----------|
| `manage-email` | Act as email administrator | None |
| `draft-email` | Draft a new email | content, recipient, recipient_email |
| `edit-draft` | Edit existing email draft | changes, current_draft |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
