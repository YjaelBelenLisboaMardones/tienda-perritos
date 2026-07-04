# ── Stage 1: preparación de archivos ──────────────────── 
FROM node:18-alpine AS builder 
WORKDIR /app 
COPY . . 
# ── Stage 2: imagen de producción (Nginx) ─────────────── 
FROM nginx:alpine AS runner 
COPY --from=builder /app/index.html /usr/share/nginx/html/ 
COPY --from=builder /app/app.js    /usr/share/nginx/html/ 
COPY default.conf /etc/nginx/conf.d/default.conf 
EXPOSE 80 
CMD ["nginx", "-g", "daemon off;"]