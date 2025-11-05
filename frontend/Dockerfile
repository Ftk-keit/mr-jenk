# Build optimisé avec cache
FROM node:22-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --prefer-offline --no-audit && npm install -g @angular/cli
COPY . .
EXPOSE 4200
CMD ["ng", "serve", "--host", "0.0.0.0", "--port", "4200"]
