FROM node:22-alpine

ENV NODE_ENV=production
ENV PORT=9000

WORKDIR /app

COPY package*.json ./
RUN npm ci --omit=dev

COPY server.js relay.js push-service.js apns-client.js ./

RUN mkdir -p /data && chown -R node:node /data

USER node

EXPOSE 9000

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 CMD node -e "const port = process.env.PORT || 9000; fetch('http://127.0.0.1:' + port + '/health').then((res) => process.exit(res.ok ? 0 : 1)).catch(() => process.exit(1))"

CMD ["npm", "start"]
