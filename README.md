# render-webrtc-signal-server

Render.com host for [`@papit/signal-server`](https://github.com/onkelhoy/papit/tree/main/packages/network/signal-server), the signalling relay the [webrtc demo](https://onkelhoy.github.io/webrtc-demo/) connects to.

Live: `wss://render-webrtc-signal-server.onrender.com` (health: `https://render-webrtc-signal-server.onrender.com/health`)

## Render settings

| Setting | Value |
|---|---|
| Service type | Web Service, Node |
| Build command | `npm install` |
| Start command | `npm start` |
| Health check path | `/health` |

The server reads the port from Render's `PORT` env variable. Optional flags can be appended to the start command, e.g. `npm start -- --forward-rate=300`; see the signal-server README for the full list.

On the free plan the service sleeps when idle and takes a while to wake. The client shows `waking` and keeps retrying (it pings `/health` to speed the wake-up), so just wait for it to connect.

## Run locally

```bash
npm install
PORT=3000 npm start
```
