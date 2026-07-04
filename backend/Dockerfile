# ── Stage 1: instalación de dependencias ───────────────── 
FROM node:18-alpine AS builder 
WORKDIR /app 
COPY package*.json ./ 
RUN npm ci --only=production 
# ── Stage 2: imagen de producción ──────────────────────── 
FROM node:18-alpine AS runner 
# Usuario no root por seguridad (mínimo privilegio) 
RUN addgroup -S appgroup && adduser -S appuser -G appgroup 
WORKDIR /app 
COPY --from=builder /app/node_modules ./node_modules 
COPY . . 
USER appuser 
EXPOSE 3001 
CMD ["node", "server.js"] 