FROM node:slim

ENV DB_DATABASE=kubedevnews \
    DB_USERNAME=kubedevnews \
    DB_PASSWORD=Pg#123 \
    DB_HOST=postgres

WORKDIR /app

COPY package.json .

RUN npm install

EXPOSE 8080

COPY . .

CMD ["node", "server.js"]


