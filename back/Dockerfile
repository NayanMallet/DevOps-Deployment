# Étape 1 : Build des dépendances dans une image temporaire
FROM node:18-alpine AS build

RUN apk add --no-cache openssl1.1-compat || apk add --no-cache openssl

WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci --only=production  # Installe uniquement les dépendances nécessaires
COPY . .

# Étape 2 : Image finale, on ne garde que l'essentiel
FROM node:18-alpine

WORKDIR /app
COPY --from=build /app /app
RUN addgroup -S appgroup && adduser -S appuser -G appgroup \
    && chown -R appuser:appgroup /app
USER appuser

EXPOSE 3000

CMD ["sh", "-c", "npx prisma generate && npx prisma db push && npm run start"]
#CMD ["npm", "run", "start"]
