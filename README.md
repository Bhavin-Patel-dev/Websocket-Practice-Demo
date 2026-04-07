# 🔌 WebSocket Broadcast Console

A real-time WebSocket demo app built with **Node.js** and the **`ws`** library. This project demonstrates how WebSocket connections work under the hood — from the initial handshake to live bidirectional message broadcasting across multiple connected clients.

---

## 📌 Purpose

This project was built as a hands-on learning exercise to understand:

- How the WebSocket protocol differs from HTTP
- How a Node.js server manages multiple simultaneous client connections
- How messages are broadcast to all connected clients in real time
- How to build and serve a minimal WebSocket-powered frontend

It serves as a clean, minimal reference for anyone getting started with WebSockets in Node.js.

---

## ✨ Features

- ⚡ Real-time bidirectional communication over WebSocket

- 📡 Server broadcasts every message to **all connected clients**

- 🖥️ Built-in browser client — no external frontend framework needed

- 🧱 Single-port architecture — HTTP and WebSocket share the same server

- 🪵 Timestamped live stream logs in the UI

---

## 🛠️ Tech Stack

| Layer            | Technology                                  |
| ---------------- | ------------------------------------------- |
| Runtime          | Node.js (ES Modules)                        |
| WebSocket Server | [`ws`](https://github.com/websockets/ws) v8 |
| HTTP Server      | Node.js built-in `http` module              |
| Frontend         | Vanilla HTML + CSS + JavaScript             |

---

## 🗂️ Project Structure

```
Websocket-Practice-Demo/
├── server.js        # WebSocket + HTTP server
├── index.html       # Browser client (UI + WebSocket client logic)
├── package.json     # Project metadata and scripts
├── .gitignore       # Ignores node_modules
└── README.md        # Project documentation
```

---

## ⚙️ How It Works

### 1. The Handshake

When a browser loads `index.html`, it initiates a WebSocket handshake with the server by sending an HTTP `Upgrade` request. The server upgrades the connection from HTTP to the WebSocket protocol — this is a persistent, full-duplex TCP connection.

```
Browser                        Server
  |                               |
  |  -- HTTP Upgrade Request -->  |
  |  <-- 101 Switching Protocols--|
  |                               |
  |  <===== WS Connection ======> |  (stays open)
```

### 2. Message Broadcasting

When any connected client sends a message, the server iterates over **all active clients** and forwards the message to each one — including the sender. This is the core broadcast pattern.

```javascript
wss.clients.forEach((client) => {
  if (client.readyState === WebSocket.OPEN)
    client.send(`Server Broadcast: ${message}`);
});
```

---

## 🧑‍💻 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or higher
- npm

### Installation

```bash
# Clone the repository
git clone https://github.com/Bhavin-Patel-dev/Websocket-Practice-Demo.git

# Navigate into the project
cd Websocket-Practice-Demo

# Install dependencies
npm install
```

### Running Locally

```bash
# Start the server
npm start

# Or with auto-restart on file changes (development)
npm run dev
```

Open your browser and go to:

```
http://localhost:8080
```

### Testing with wscat (Optional CLI tool)

```bash
npx wscat -c ws://localhost:8080
```

Type any message and hit Enter — you'll see it broadcast back from the server.

---

## 📜 Available Script

| Script | Command                  | Description                        |
| ------ | ------------------------ | ---------------------------------- |
| `dev`  | `node --watch server.js` | Start with auto-restart on changes |

---

## 🔍 WebSocket vs HTTP — Quick Comparison

|            | HTTP                         | WebSocket                |
| ---------- | ---------------------------- | ------------------------ |
| Connection | Opens and closes per request | Stays open persistently  |
| Direction  | Client → Server only         | Full duplex (both ways)  |
| Overhead   | Headers sent every request   | Minimal after handshake  |
| Use case   | REST APIs, page loads        | Chat, live feeds, gaming |

---

> Built with curiosity and a lot of `wscat` 🔌
