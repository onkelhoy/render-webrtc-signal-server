# render-webrtc-signal-server

Render.com host for [`@papit/signal-server`](https://github.com/onkelhoy/papit/tree/main/packages/network/signal-server), the signalling relay the [webrtc demo](https://onkelhoy.github.io/webrtc-demo/) connects to.

Live: [render-webrtc-signal-server.onrender.com](https://render-webrtc-signal-server.onrender.com/health) (socket: `wss://render-webrtc-signal-server.onrender.com`, health: `https://render-webrtc-signal-server.onrender.com/health`)

## Environment variables

Set these in the Render dashboard under **Environment**. Never commit them, this repo is public.

| Variable | Required | Description |
|---|---|---|
| `VAPID_PUBLIC_KEY` | for web push | public half of the key pair |
| `VAPID_PRIVATE_KEY` | for web push | private half, keep it secret |
| `VAPID_SUBJECT` | no | `mailto:` or `https:` contact shown to push services, defaults to the papit repo |

Generate the pair once with `npx @papit/signal-server --generate-vapid` and keep it: new keys void every push token. Without them the server still runs, on throwaway keys that die on restart. Render sets `PORT` itself.

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
