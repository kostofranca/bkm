FROM node

RUN mkdir -p /home/gantek/app/node_modules && chown -R node:node /home/gantek/app

WORKDIR /home/gantek/app

COPY package*.json ./

USER root

RUN npm install

COPY --chown=node:node . .

CMD [ "node", "index.js" ]
