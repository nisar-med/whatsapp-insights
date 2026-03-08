# Development Guide

## Architecture

- Frontend: Next.js App Router (`app/page.tsx`)
- API route: Next.js route handler for AI (`app/api/ai/route.ts`)
- Realtime + WhatsApp bridge: Express + Socket.IO + Baileys (`server.ts`)
- Session auth storage: `auth_info/<sid>/...`

The server process starts Express and Next.js together, then handles:

- WhatsApp socket lifecycle
- Session validation and cleanup
- Realtime message/chat broadcast to clients in `session:<sid>` rooms

## Scripts

| Script | Description |
| --- | --- |
| `npm run dev` | Start development server with `tsx watch server.ts` |
| `npm run build` | Build Next.js app |
| `npm run build:server` | Compile `server.ts` to `dist/` |
| `npm run start` | Start server entrypoint (`server.ts`) |
| `npm run lint` | Run ESLint |

## Session And Data Management

- Session ids are validated against `^[a-zA-Z0-9_-]{8,128}$`
- Message cache is capped (default 1000 items)
- Idle sessions are cleaned up from memory after inactivity
- Session auth files are retained unless an explicit reset removes them

> [!WARNING]
> Do not share or commit the `auth_info/` directory. It can contain active credentials and device linkage data.

## Tech Stack

Next.js, React, TypeScript, Express, Socket.IO, Baileys, Google GenAI, Tailwind CSS.
