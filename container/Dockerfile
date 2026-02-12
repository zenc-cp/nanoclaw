FROM node:22-slim

WORKDIR /app
COPY package*.json ./
RUN npm install && npm run build
COPY . .

# Data persistence
RUN mkdir -p /app/data /workspace/group /workspace/global /app/env-dir
VOLUME ["/app/data", "/workspace/group", "/workspace/global"]

EXPOSE 10000
CMD ["npm", "start"]
