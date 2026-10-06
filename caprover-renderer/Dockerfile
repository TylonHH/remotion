FROM node:22-bookworm-slim
WORKDIR /app
ENV NODE_ENV=production PORT=3000 OUTPUT_DIR=/data/renders
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates fonts-liberation libasound2 libatk-bridge2.0-0 libatk1.0-0 libcups2 libdbus-1-3 libdrm2 libgbm1 libglib2.0-0 libgtk-3-0 libnspr4 libnss3 libx11-6 libxcomposite1 libxdamage1 libxext6 libxfixes3 libxkbcommon0 libxrandr2 xdg-utils && rm -rf /var/lib/apt/lists/*
COPY caprover-renderer/package.json ./
# Install Chrome through the pinned renderer API; this service does not ship the CLI.
RUN npm install --omit=dev && node --input-type=module -e "import {ensureBrowser} from '@remotion/renderer'; await ensureBrowser();"
COPY caprover-renderer/server.mjs ./
RUN mkdir -p /data/renders
EXPOSE 3000
VOLUME ["/data/renders"]
CMD ["npm","start"]
