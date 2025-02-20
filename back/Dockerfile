FROM node:18 AS build-back

WORKDIR /app
COPY package*.json ./
RUN npm install

# Copie du reste du code
COPY . .

EXPOSE 3000

CMD ["sh", "-c", "npx prisma db push && npm run start"]
#CMD ["npm", "run", "start"]
