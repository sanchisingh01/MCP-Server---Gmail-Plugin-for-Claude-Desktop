# Gmail Plugin MCP Server

[![Python Version](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

A powerful MCP server that enables Gmail integration, allowing you to manage emails directly through MCP clients. This plugin provides seamless access to Gmail's core functionality including reading, sending, and managing emails.

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

2. Install dependencies:
```bash
uv pip install -e .
```

3. Configure your Gmail API credentials:
   - Go to [Google Cloud Console](https://console.cloud.google.com)
   - Create a new project or select existing one
   - Enable Gmail API
   - Create OAuth 2.0 credentials
   - Download the credentials file, rename it and copy the absolute path of credentials file. This will be passed as parameter in --cred-file-path
   - 

### Configuration

#### For Development/Unpublished Servers

Add this to your MCP client configuration (for Claude Desktop) : claude_desktop_config.json

```json
"mcpServers": {
  "gmail-plugin": {
    "command": "uv",
    "args": [
      "--directory",
      [absolute path to working directory],
      "run",
      "server.py"
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
