# FROM node:20-alpine AS build
# WORKDIR /app
# COPY package*.json ./
# RUN npm ci
# COPY . .

# FROM node:20-alpine AS final
# WORKDIR /app
# COPY package*.json ./
# RUN npm ci --omit=dev && npm cache clean --force
# COPY --from=build /app/server.js .

# ARG UID=10001
# RUN adduser \
#     --disabled-password \
#     --gecos "" \
#     --home "/nonexistent" \
#     --shell "/sbin/nologin" \
#     --no-create-home \
#     --uid "${UID}" \
#     appuser
# USER appuser

# EXPOSE 8081
# CMD ["node", "server.js"]


FROM node:22-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm ci --omit=dev

COPY . .

FROM gcr.io/distroless/nodejs22-debian13:nonroot AS final

WORKDIR /app

COPY --from=build --chown=nonroot:nonroot /app/ /app/

ENV NODE_ENV=production

EXPOSE 8081

CMD ["server.js"]
