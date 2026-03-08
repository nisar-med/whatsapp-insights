# WhatsApp Insights

Real-time WhatsApp message sync and AI-powered chat analysis in a single web app.

WhatsApp Insights connects to your WhatsApp account through a QR login flow, streams recent messages into a local session cache, and lets you ask natural-language questions over that message context using Gemini.

> [!IMPORTANT]
> This project stores WhatsApp authentication and session artifacts locally under `auth_info/`. Keep that directory private and never commit credentials.

## Features

- QR-based WhatsApp device linking
- Real-time message synchronization
- AI-powered chat Q&A using Gemini
- Multi-session support
- Local message persistence

## Prerequisites

- Node.js 22+
- npm
- A Gemini API key

## Installation

### Option 1: Run as a Package

Set your Gemini API key first:

```bash
export GEMINI_API_KEY="your_api_key_here"
```

Then install and run globally:

```bash
npm install -g whatsapp-insights@latest
whatsapp-insights
```

Or run without installation:

```bash
npx whatsapp-insights@latest
```

### Option 2: Run from Source

1. Clone the repository:

```bash
git clone https://github.com/nisar-med/whatsapp-insights.git
cd whatsapp-insights
```

2. Install dependencies:

```bash
npm install
```

3. Configure your Gemini API key:

```bash
cp .env.example .env.local
```

Edit `.env.local` and set your `GEMINI_API_KEY`:

```bash
GEMINI_API_KEY="your_api_key_here"
```

4. Start the application:

```bash
npm run dev
```

## Usage

1. Open your browser and navigate to `http://localhost:3000`
2. Scan the QR code with WhatsApp on your phone:
   - Open WhatsApp on your phone
   - Tap Menu or Settings → Linked Devices
   - Tap "Link a Device"
   - Point your phone at the QR code
3. Once connected, your messages will sync automatically
4. Ask questions about your chats in the AI Assistant panel

> [!TIP]
> If the QR code expires, click the "Retry" button to generate a new one.

## Environment Variables

| Variable | Required | Description |
| --- | --- | --- |
| `GEMINI_API_KEY` | Yes | Your Google Gemini API key for AI features |

Example setup:

**macOS/Linux:**
```bash
export GEMINI_API_KEY="your_api_key_here"
```

**Windows (PowerShell):**
```powershell
$env:GEMINI_API_KEY="your_api_key_here"
```

## Troubleshooting

**Connection Issues:**
- Ensure your phone has an active internet connection
- Try clicking "Reset Session" to start fresh
- Make sure you're scanning the QR code from the latest version of WhatsApp

**API Errors:**
- `Gemini API key is not configured`: Set the `GEMINI_API_KEY` environment variable and restart the application
- Empty AI responses: Wait for messages to sync before asking questions

**QR Code Expired:**
- Click the "Retry" button to generate a fresh QR code
- QR codes expire after a few minutes for security

## Documentation

- [API Reference](docs/api.md) - REST and Socket.IO API documentation
- [Development Guide](docs/development.md) - Architecture and development setup

## Tech Stack

Next.js, React, TypeScript, Express, Socket.IO, Baileys, Google GenAI, Tailwind CSS.
