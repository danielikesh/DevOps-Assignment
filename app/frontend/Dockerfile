FROM node:18-alpine

WORKDIR /app

COPY frontend/package*.json ./
RUN npm install

COPY frontend/ .

ENV PORT=3000
EXPOSE 3000

CMD ["npm", "run", "start"]