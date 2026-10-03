# CapRover Remotion Renderer

HTTP rendering service for Remotion, intended for CapRover and n8n.

## CapRover
Deploy the GHCR image, set container port to `3000`, and map persistent storage to `/data/renders`.

Environment: `API_KEY` (recommended), `PORT=3000`, `OUTPUT_DIR=/data/renders`.

## API
`GET /health`

`POST /render` with Bearer authentication:

```json
{"serveUrl":"https://your-remotion-bundle.example/","compositionId":"Reel","inputProps":{"hook":"Dein Kind hört nie auf dich?"},"codec":"h264","concurrency":2}
```

Poll `GET /jobs/:id`. When status is `done`, download the MP4 from `/renders/<id>.mp4`.

## n8n
Use HTTP Request to POST `/render`, then poll `/jobs/:id`. The same image can run on CapRover or beside n8n.

## Security
Do not expose `/render` without `API_KEY`. Only use trusted Serve URLs.
