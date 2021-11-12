FROM node:16-alpine as builder

USER node
RUN mkdir -p /home/app/node
WORKDIR '/home/app/node'

COPY --chown=node:node ./package.json ./
RUN npm install
COPY --chown=node:node . .

RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /home/app/node/build /usr/share/nginx/html