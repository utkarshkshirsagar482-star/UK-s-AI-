# MCP Host - Web-based AI Chat Application

## Overview
A web-based MCP (Model Context Protocol) host application similar to Fire or LM Studio. The application enables users to interact with AI models through OpenRouter API, manage custom API keys, configure MCP servers via JSON, and engage in real-time chat conversations.

## Project Purpose
Provide developers with a powerful, web-based interface to:
- Connect to OpenRouter-compatible AI models (GPT-4, Claude, etc.)
- Manage multiple API keys securely
- Configure MCP servers through JSON file uploads
- Chat with AI in real-time with streaming responses
- Monitor server status and connections

## Architecture
**Stack**: Full-stack JavaScript (Node.js + React)
- Frontend: React with Wouter routing, TanStack Query, Shadcn UI components
- Backend: Express.js with WebSocket support for real-time streaming
- Storage: In-memory storage (MemStorage) for sessions and configurations
- Real-time: WebSocket connection for chat streaming

## Core Features (MVP)
1. **Chat Interface**: Real-time chat with AI models, streaming responses, message history
2. **API Key Management**: Add, store, test, and delete OpenRouter API keys
3. **MCP Server Configuration**: Upload and validate JSON configuration files
4. **Model Selection**: Choose from available OpenRouter models
5. **Server Status**: Display connected MCP servers and their status
6. **Clean UI**: Split-panel layout with sidebar navigation and main content area

## Recent Changes
- 2025-01-24: Project initialized with design guidelines

## User Preferences
- Prefers developer-focused, functional UI similar to Linear/GitHub
- Wants web-based solution (not desktop)
- Needs OpenRouter API compatibility
- Requires JSON-based MCP server configuration

## Project Structure
```
client/
  src/
    components/     # Reusable UI components
    pages/          # Page components (Chat, API Keys, MCP Servers, Settings)
    lib/            # Utilities and helpers
server/
  routes.ts         # API routes and WebSocket setup
  storage.ts        # In-memory data storage
shared/
  schema.ts         # Data models and TypeScript interfaces
```

## Technical Details
- WebSocket path: `/ws` for real-time chat streaming
- API prefix: `/api` for all REST endpoints
- Design system: Custom tokens in tailwind.config.ts following design_guidelines.md
