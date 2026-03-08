# API Reference

## WhatsApp Session Endpoints

All WhatsApp session endpoints require a valid `sid` query parameter.

### GET /api/whatsapp/messages

Return cached messages for the session.

**Query Parameters:**
- `sid` (required): Session identifier

**Response:**
```json
[
  {
    "id": "message_id",
    "remoteJid": "1234567890@s.whatsapp.net",
    "pushName": "John Doe",
    "text": "Hello world",
    "timestamp": 1234567890
  }
]
```

### GET /api/whatsapp/status

Return connection status and user metadata.

**Query Parameters:**
- `sid` (required): Session identifier

**Response:**
```json
{
  "status": "connected",
  "user": {
    "id": "1234567890@s.whatsapp.net",
    "name": "My WhatsApp"
  }
}
```

### POST /api/whatsapp/retry

Retry WhatsApp connection when disconnected or QR expired.

**Query Parameters:**
- `sid` (required): Session identifier

**Response:**
```json
{
  "success": true
}
```

### POST /api/whatsapp/reset

Logout/reset session auth and reconnect.

**Query Parameters:**
- `sid` (required): Session identifier

**Response:**
```json
{
  "success": true
}
```

### POST /api/session

Create or register a session id.

**Request Body:**
```json
{
  "sid": "optional_existing_session_id"
}
```

**Response:**
```json
{
  "sid": "session_id"
}
```

### POST /api/ai

Generate AI answer from provided message context and query.

**Request Body:**
```json
{
  "sid": "session_id",
  "query": "What did John say yesterday?",
  "messages": [
    {
      "remoteJid": "1234567890@s.whatsapp.net",
      "pushName": "John Doe",
      "text": "Hello world",
      "timestamp": 1234567890
    }
  ]
}
```

**Response:**
```json
{
  "answer": "Based on the messages, John said 'Hello world'."
}
```

**Rate Limits:**
- 20 requests per minute per session
- Returns `429 Too Many Requests` with `Retry-After` header when exceeded

## Socket.IO Events

Connect with `auth: { sid: "session_id" }` or `query: { sid: "session_id" }`.

### Client → Server

None (read-only connection)

### Server → Client

- `whatsapp:status`: Connection status changed (`connecting`, `connected`, `disconnected`, `qr_timeout`)
- `whatsapp:qr`: New QR code available (data URL)
- `whatsapp:messages`: Full message cache sync
- `whatsapp:new_message`: New message received
- `whatsapp:chats`: Chat list update
- `whatsapp:error`: Error message
