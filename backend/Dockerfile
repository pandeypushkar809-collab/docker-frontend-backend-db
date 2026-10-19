FROM node:22-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm ci --omit=dev
COPY . .

FROM alpine:3.24 AS runtime

RUN apk add --no-cache libstdc++ dumb-init \
    && addgroup -S app \
    && adduser -S -G app app

WORKDIR /app

COPY --from=build /usr/local/bin/node /usr/local/bin/node
COPY --from=build --chown=app:app /app/node_modules ./node_modules
COPY --from=build --chown=app:app /app/server.js ./server.js
COPY --from=build --chown=app:app /app/routes ./routes
COPY --from=build --chown=app:app /app/models ./models

USER app
EXPOSE 3001
CMD ["dumb-init", "node", "server.js"]
