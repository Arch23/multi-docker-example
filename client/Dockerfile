FROM node:14.14.0-alpine as builder

USER node

RUN mkdir -p /home/node/app
WORKDIR '/home/node/app'
COPY --chown=node:node ./package.json ./
RUN npm install

COPY --chown=node:node . .

CMD ["npm", "run", "build"]

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /home/node/app /usr/share/nginx/html