# crdt-signaler-yjs

**crdt-signaler-yjs** is a signaling server built using Yjs, designed to handle real-time collaborative editing for your SaaS application **Octaview**. This server allows multiple users to edit code collaboratively in real time through a powerful, efficient CRDT (Conflict-Free Replicated Data Types) mechanism.

## Features

- Real-time collaboration for editing code
- Built on Yjs for CRDT-based synchronization
- Easily integrates with **Octaview**, a collaborative hiring and interview platform
- Designed to work with **Monsco**, a collaborative code editor, within the **Octaview** platform
- Efficient signaling for WebRTC-based peer-to-peer communication

## How It Works

The `crdt-signaler-yjs` server facilitates the signaling process for WebRTC peer connections. It ensures that multiple users can join the same room and start collaborating in real-time, without losing synchronization. This is achieved by utilizing Yjs, which maintains consistency between users' states during the collaborative editing process.

## Installation

### Prerequisites

Before starting, make sure you have the following installed:

- **Node.js** (v14 or above)
- **NPM** or **Yarn**
- A **WebSocket** server (or other signaling protocol setup)

### Steps to Install

Follow these steps to set up the signaling server:

1. Clone the repository:

   ```
   git clone https://github.com/<your-username>/crdt-signaler-yjs.git
   cd crdt-signaler-yjs
   ```

```import \* as Y from 'yjs'
import { WebrtcProvider } from 'y-webrtc'

const ydoc = new Y.Doc()
//clients connected to the same room-name share document updates
const provider = new WebrtcProvider('your-room-name', ydoc, { password: 'optional-room-password' })
const yarray = ydoc.get('array', Y.Array)```

### Signaling

The peers find each other by connecting to a signaling server. This package implements a small signaling server in `./bin/server.js`.

```sh
# start signaling server
PORT=4444 node ./bin/server.js
```

Peers using the same signaling server will find each other. You can specify several custom signaling servers like so:

```js
const provider = new WebrtcProvider("your-room-name", ydoc, {
  signaling: ["wss://y-webrtc-ckynwnzncc.now.sh", "ws://localhost:4444"],
});
```

## Integration with Octaview

Octaview is a collaborative hiring and interview platform that integrates various tools to enhance the recruitment process. One of the core features of Octaview is the Collaborative Code Editor, built using Monco VS Code, which allows real-time collaboration on code editing.

The crdt-signaler-yjs server plays a crucial role in enabling real-time collaboration by managing WebRTC peer connections within the Octaview platform. It allows users to collaborate seamlessly in the Collaborative Code Editor.

### Steps to Integrate

Integrate Monco VS Code as the code editor: Set up the Monco VS Code collaborative code editor within Octaview.
Use the signaling server: Configure your Octaview platform to interact with the crdt-signaler-yjs server for managing WebRTC peer connections.
Real-time updates: The server will ensure that all changes are reflected in real-time during collaboration in Monco VS Code.

## License

For more information about Octaview and its features, visit the Octaview Website.

**crdt-signaler-yjs** is a wrapper around Yjs, utilizing its CRDT capabilities for real-time collaborative editing.

Yjs is licensed under the [MIT License](./LICENSE).
